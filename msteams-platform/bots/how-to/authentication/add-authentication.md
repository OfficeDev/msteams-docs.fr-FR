---
title: Ajouter l’authentification à votre bot Teams
author: surbhigupta
description: Découvrez comment activer l’authentification à l’aide d’un fournisseur OAuth tiers pour une application bot dans Teams à l’aide d’Azure AD.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: ff7e4e8d3ffede250bd89ecca7b0e3d8054a646b
ms.sourcegitcommit: 0ac53c430c055897ecebc129eab49336820c18c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67618330"
---
# <a name="add-authentication-to-your-teams-bot"></a>Ajouter l’authentification à votre bot Teams

Il peut arriver que vous deviez créer des bots dans Microsoft Teams qui peuvent accéder aux ressources pour le compte de l’utilisateur, comme un service de messagerie.

Cet article montre comment utiliser l’authentification SDK Azure Bot Service v4, basée sur OAuth 2.0. Cela facilite le développement d’un bot qui peut utiliser des jetons d’authentification basés sur les informations d’identification de l’utilisateur. La clé dans tout cela est l’utilisation de **fournisseurs d’identité**, comme nous le verrons plus loin.

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Microsoft Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base du flux d’octroi implicite OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans les onglets Microsoft Teams.

Consultez [OAuth 2 Simplifié](https://aka.ms/oauth2-simplified) pour une compréhension de base, et [OAuth 2.0](https://oauth.net/2/) pour la spécification complète.

Pour plus d’informations sur la façon dont Azure Bot Service gère l’authentification, consultez [l’authentification utilisateur dans une conversation](https://aka.ms/azure-bot-authentication).

Voici les titres des sections de cet article :

- **Comment créer un bot prenant en charge l’authentification**. Vous allez utiliser [cs-auth-sample][teams-auth-bot-cs] pour gérer les informations d’identification de connexion utilisateur et la génération du jeton d’authentification.
- **Comment déployer le bot sur Azure et l’associer à un fournisseur d’identité**. Le fournisseur émet un jeton basé sur les informations d’identification de connexion de l’utilisateur. Le bot peut utiliser le jeton pour accéder aux ressources, telles qu’un service de messagerie, qui nécessitent une authentification. Pour plus d’informations, consultez  [le flux d’authentification Microsoft Teams pour les bots](auth-flow-bot.md).
- **Comment intégrer le bot dans Microsoft Teams**. Une fois le bot intégré, vous pouvez vous connecter et échanger des messages avec lui dans une conversation.

## <a name="prerequisites"></a>Configuration requise

- Connaissance des [principes de base du bot][concept-basics], [de la gestion de l’état][concept-state], de la [bibliothèque de dialogues][concept-dialogs] et de la façon d’implémenter un [flux de conversation séquentiel][simple-dialog].
- Connaissance du développement Azure et OAuth 2.0
- Les versions actuelles de Microsoft Visual Studio et Git.
- Accédez à votre compte Azure. Si nécessaire, vous pouvez créer un [compte gratuit Azure](https://azure.microsoft.com/free/).
- L’exemple suivant :

    | Échantillon | Version de BotBuilder | Démontre |
    |:---|:---:|:---|
    | **Authentification de bot** dans [cs-auth-sample][teams-auth-bot-cs] | v3, v4 | Prise en charge d’OAuthCard |
    | **Authentification de bot** dans [js-auth-sample][teams-auth-bot-js] | v3, v4| Prise en charge d’OAuthCard  |
    | **Authentification de bot** dans [py-auth-sample][teams-auth-bot-py] | v3, v4 | Prise en charge d’OAuthCard |

## <a name="create-the-resource-group"></a>Créer le groupe de ressources

Le groupe de ressources et le plan de service ne sont pas strictement nécessaires, mais ils vous permettent de libérer facilement les ressources que vous créez. Il s’agit d’une bonne pratique pour garder vos ressources organisées et gérables.

Vous utilisez un groupe de ressources pour créer des ressources individuelles pour Bot Framework. Pour des raisons de performances, assurez-vous que ces ressources se trouvent dans la même région Azure.

1. Dans votre navigateur, connectez-vous au [**portail Microsoft Azure**][azure-portal].
1. Dans le volet de navigation gauche, sélectionnez **Groupes de ressources**.
1. Dans le coin supérieur gauche de la fenêtre affichée, sélectionnez **Ajouter** un onglet pour créer un groupe de ressources. Vous êtes invité à fournir les éléments suivants :
    1. **Abonnement**. Utilisez votre abonnement existant.
    1. **Groupe de ressources** Entrez le nom de l’image et le groupe de ressources. *Par exemple, TeamsResourceGroup* N’oubliez pas que le nom doit être unique.
    1. Dans le menu déroulant **Région** , sélectionnez *USA Ouest* ou une région proche de vos applications.
    1. Sélectionnez le bouton **Vérifier et créer** . Vous devriez voir une bannière qui lit *Validation réussie*.
    1. Sélectionnez le bouton **Créer**. La création du groupe de ressources peut prendre quelques minutes.

> [!TIP]
> Comme avec les ressources que vous allez créer plus loin dans ce didacticiel, il est judicieux d’épingler ce groupe de ressources à votre tableau de bord pour faciliter l’accès. Si vous le souhaitez, sélectionnez l’icône épingler &#128204; en haut à droite du tableau de bord.

## <a name="create-the-service-plan"></a>Créer le plan de service

1. Dans le [**Portail Azure**][azure-portal], dans le volet de navigation gauche, sélectionnez **Créer une ressource**.
1. Dans la zone de recherche, tapez *App Service Plan*. Sélectionnez la **carte plan App Service** dans les résultats de la recherche.
1. Sélectionnez **Créer**.
1. Il vous sera demandé de fournir les informations suivantes :
    1. **Abonnement**. Vous pouvez utiliser un abonnement existant.
    1. **Groupe de ressources** Sélectionnez la base de données de mappages que vous avez créée précédemment.
    1. **Nom**. Entrez le nom du plan de service. *Par exemple, TeamsServicePlan*. N’oubliez pas que le nom doit être unique, au sein du groupe.
    1. **Système d’exploitation** Sélectionnez *Windows* ou votre système d’exploitation applicable.
    1. **Région** Sélectionnez *USA Ouest* ou une région proche de vos applications.
    1. **Niveau tarifaire** Vérifiez que *Standard S1* est sélectionné. Il doit s’agir de la valeur par défaut.
    1. Sélectionnez le bouton **Vérifier et créer** . Vous devriez voir une bannière qui lit *Validation réussie*.
    1. Sélectionnez **Créer**. La création du plan App Service peut prendre quelques minutes. Le plan est répertorié dans le groupe de ressources.

## <a name="create-azure-bot-resource-registration"></a>Créer une inscription de ressource Azure Bot

L’inscription des ressources Azure Bot inscrit votre service web en tant que bot auprès de Bot Framework, qui vous fournit un ID d’application Microsoft et un mot de passe d’application (clé secrète client).

> [!IMPORTANT]
> Vous n’avez besoin d’inscrire votre bot que s’il n’est pas hébergé dans Azure. Si vous [avez créé un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) via le Portail Azure il est déjà inscrit auprès du service. Si vous avez créé votre bot via [Bot Framework](https://dev.botframework.com/bots/new) ou le [portail des développeurs,](../../../concepts/build-and-test/teams-developer-portal.md) votre bot n’est pas inscrit dans Azure.

1. Visitez [**Portail Azure**][azure-portal] et recherchez **Azure Bot** dans **la section Créer une ressource**.
1. Ouvrez Le **bot Azure** , puis **sélectionnez Créer**.
1. Entrez le nom du handle du bot dans le champ **Descripteur** de bot.
1. Sélectionnez votre **abonnement** dans la liste déroulante.
1. Sélectionnez votre **groupe de ressources** dans la liste déroulante.
1. Sélectionnez **Type d’application** en tant que **multilocataire** pour **l’ID d’application Microsoft**.

   :::image type="content" source="../../../assets/images/adaptive-cards/multi-tenant.png" alt-text="Cette capture d’écran montre comment sélectionner plusieurs locataires pour Microsoft AppID.":::

1. Sélectionnez **Examiner et créer**.

   :::image type="content" source="../../../assets/images/adaptive-cards/create-azure-bot.png" alt-text="Cette capture d’écran montre comment créer un bot Azure.":::

1. Si la validation réussit, sélectionnez **Créer**.

    L’approvisionnement de votre service de bot prend quelques instants.

   :::image type="content" source="../../../assets/images/adaptive-cards/validation-pane.png" alt-text="Cette capture d’écran montre comment la validation du bot Azure réussit.":::

1. Sélectionnez **Accéder à la ressource**. Le bot et les ressources associées sont répertoriés dans le groupe de ressources.

   :::image type="content" source="../../../assets/images/adaptive-cards/go-to-resource-card.png" alt-text="Cette capture d’écran montre comment sélectionner un groupe de ressources.":::

    Votre bot Azure est maintenant créé.

   :::image type="content" source="../../../assets/images/adaptive-cards/azure-bot-ui.png" alt-text="Cette capture d’écran montre comment créer des ressources de bot Azure.":::

Pour créer une clé secrète client :

1. Dans **Paramètres**, sélectionnez **Configuration**. Enregistrez **l’ID d’application Microsoft** (ID client) pour référence ultérieure.

   :::image type="content" source="../../../assets/images/adaptive-cards/config-microsoft-app-id.png" alt-text="Cette capture d’écran montre comment ajouter l’ID d’application Microsoft pour créer une clé secrète client.":::

1. En regard de **l’ID d’application Microsoft**, **sélectionnez Gérer**.

   :::image type="content" source="~/assets/images/manage-bot-label.png" alt-text="Cette capture d’écran montre comment créer un bot de gestion.":::

1. Dans la section **Secrets client** , sélectionnez **Nouvelle clé secrète client**. **Une fenêtre de clé secrète client** s’affiche.

   :::image type="content" source="../../../assets/images/meetings-side-panel/newclientsecret.PNG" alt-text="Cette capture d’écran montre comment créer une clé secrète client.":::

1. Entrez **Description** , puis **sélectionnez Ajouter**.

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="La capture d’écran montre comment entrer la description de la clé secrète client.":::

1. Dans la colonne **Valeur** , sélectionnez **Copier dans le Presse-papiers** et enregistrez l’ID de clé secrète client pour référence ultérieure.

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret-value.png" alt-text="La capture d’écran montre comment enregistrer l’ID de clé secrète client pour une référence ultérieure.":::

Pour ajouter le canal Microsoft Teams :

1. Accéder à **l’Accueil**

   :::image type="content" source="../../../assets/images/adaptive-cards/bot-home-page.png" alt-text="Cette capture d’écran montre la page d’accueil du bot.":::

1. Ouvrez votre bot, qui est répertorié dans la section **Ressources récentes** .

1. Sélectionnez **Canaux** dans le volet gauche, puis **sélectionnez Microsoft Teams**:::image type="icon" source="../../../assets/icons/teams-icon.png":::.

   :::image type="content" source="../../../assets/images/adaptive-cards/channel-teams.png" alt-text="Cette capture d’écran montre comment sélectionner Teams dans les canaux.":::

1. Cochez la case pour accepter les conditions d’utilisation, puis **sélectionnez Accepter**.</br>

   :::image type="content" source="../../../assets/images/adaptive-cards/select-terms-of-service.png" alt-text="Cette capture d’écran montre comment définir les conditions d’utilisation du service.":::

1. Sélectionnez **Enregistrer**.

   :::image type="content" source="../../../assets/images/adaptive-cards/select-teams.png" alt-text="Cette capture d’écran montre comment ajouter un canal Microsoft Teams.":::

Pour plus d’informations, consultez [Créer un robot pour Microsoft Teams](../create-a-bot-for-teams.md)

## <a name="create-the-identity-provider"></a>Créer un fournisseur d’identité

Vous avez besoin d’un fournisseur d’identité qui peut être utilisé pour l’authentification.
Dans cette procédure, vous allez utiliser un fournisseur Azure AD ; d’autres fournisseurs d’identité pris en charge par Azure AD peuvent également être utilisés.

1. Dans le [**Portail Azure**][azure-portal], dans le volet de navigation gauche, sélectionnez **Azure Active Directory**.
    > [!TIP]
    > Vous devez créer et inscrire cette ressource Azure AD dans un locataire dans lequel vous pouvez donner votre consentement pour déléguer les autorisations demandées par une application.
    > Pour obtenir des instructions sur la création d’un locataire, consultez [Accéder au portail et créer un locataire](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).
1. Dans le panneau gauche, sélectionnez **...**
1. Dans le volet droit, sélectionnez l’onglet **Nouvelle inscription**, en haut à gauche.
1. Il vous sera demandé de fournir les informations suivantes :
   1. **Nom**. Entrez le nom pour la nouvelle application de service. *Par exemple, BotTeamsIdentity* N’oubliez pas que le nom doit être unique.
   1. Sélectionnez les **types de comptes pris en charge** pour votre application. Sélectionnez *Comptes dans n’importe quel annuaire organisationnel (Tout Microsoft Azure Active Directory (Azure AD) - Multilocataire) et comptes Microsoft personnels (par exemple, Skype, Xbox).*
   1. Pour **l’URI de redirection** :<br/>
       &#x2713;Sélectionner **le web**.<br/>
       &#x2713; définir l’URL sur `https://token.botframework.com/.auth/web/redirect`
   1. Sélectionnez **Inscrire**.

1. Une fois créé, Azure affiche la page **Vue d’ensemble** de l’application. Copiez et enregistrez les informations suivantes dans un fichier :

    1. La valeur de l’**ID d’application (client)** Vous utiliserez cette valeur ultérieurement comme *ID client* lorsque vous inscrirez cette application d’identité Azure auprès de votre bot.
    1. La valeur **d’ID d’annuaire** (locataire) Vous utiliserez également cette valeur ultérieurement comme *ID de locataire* pour inscrire cette application d’identité Azure auprès de votre bot.

1. Dans le volet gauche, sélectionnez **Certificats & secrets** pour créer une clé secrète client pour votre application.

   1. Sous **Secrets client**, sélectionnez &#x2795; **Nouvelle clé secrète client**.
   1. Ajoutez une description pour identifier ce secret auprès d’autres personnes que vous devrez peut-être créer pour cette application, comme *l’application d’identité bot dans Teams*.
   1. Configurez la **Date d’expiration** de votre sélection.
   1. Sélectionnez **Ajouter**.
   1. Avant de quitter cette page, **enregistrez le secret**. Vous utiliserez cette valeur ultérieurement comme *clé secrète client* lorsque vous inscrirez votre application Azure AD auprès de votre bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Configurer la connexion du fournisseur d’identité et l’inscrire auprès du bot

Remarque : il existe deux options pour les fournisseurs de services ici : Azure AD V1 et Azure AD V2.  Les différences entre les deux fournisseurs sont résumées [ici](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), mais en général, V2 offre plus de flexibilité en ce qui concerne la modification des autorisations de bot.  API Graph autorisations sont répertoriées dans le champ étendues, et à mesure que de nouvelles autorisations sont ajoutées, les bots permettent aux utilisateurs de donner leur consentement aux nouvelles autorisations lors de la prochaine connexion.  Pour V1, le consentement du bot doit être supprimé par l’utilisateur pour que de nouvelles autorisations soient demandées dans la boîte de dialogue OAuth.

#### <a name="microsoft-azure-active-directory-azure-ad-v1"></a>Prise en charge de CORS dans Microsoft Azure Active Directory (Azure AD) V1

1. Dans le [**Portail Azure**][azure-portal], sélectionnez votre groupe de ressources dans le tableau de bord.
1. Sélectionnez le lien d’inscription de votre bot.
1. Ouvrez la page de ressources et sélectionnez **Configuration** sous **Paramètres**.
1. Sélectionnez le bouton **Ajouter des paramètres de connexion OAuth** sur l’écran Configuration.
   L’image suivante affiche la sélection correspondante dans la page de ressources :

   ![Configuration de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)

1. Remplissez le formulaire comme suit :

    1. **Nom**. Entrez un nom descriptif pour la connexion. Vous allez utiliser ce nom dans votre bot dans le `appsettings.json` fichier. Par exemple, *BotTeamsAuthADv1*.
    1. **Fournisseur de services** Sélectionner la **prise en charge de CORS dans Microsoft Azure Active Directory (Azure AD)**. Une fois cette option sélectionnée, les champs spécifiques à Azure AD s’affichent.
    1. **ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Clé secrète client** Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Grant type** Entrez `authorization_code`.
    1. **URL de connexion**. Entrez `https://login.microsoftonline.com`.
    1. **ID de locataire**, entrez **l’ID d’annuaire (locataire)** que vous avez enregistré précédemment pour votre application d’identité Azure ou **commun** en fonction du type de compte pris en charge sélectionné lors de la création de l’application de fournisseur d’identité. Pour déterminer la valeur à attribuer, suivez les critères suivants :

        - Si vous avez sélectionné *comptes uniquement dans cet annuaire organisationnel (Microsoft uniquement - Locataire unique)* ou *Comptes dans n’importe quel annuaire organisationnel (Microsoft Azure Active Directory (Azure AD ) - Multilocataire),* entrez **l’ID de locataire** que vous avez enregistré précédemment pour le Microsoft Azure Active Directory (Azure) Application AD). Il s’agit du locataire associé aux utilisateurs qui peuvent être authentifiés.

        - Si vous avez sélectionné *Comptes dans un annuaire organisationnel (Tout Microsoft Azure Active Directory (Azure AD) - Comptes Microsoft multilocataires et personnels, par exemple, Skype, Xbox, Outlook)* entrez le mot **commun** au lieu d’un ID de locataire. Sinon, l’application Azure AD (Azure AD) vérifie par le biais du locataire dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.

    h. Pour **l’URL de ressource**, entrez `https://graph.microsoft.com/`. Cela n’est pas utilisé dans l’exemple de code actuel.  
    i. Laissez **les étendues** vides. L’image suivante est un exemple.

    :::image type="content" source="../../../assets/images/authentication/auth-bot-identity-connection-adv1.PNG" alt-text="Cette capture d’écran montre comment ajouter une connexion d’identité de bot d’authentification de bot Teams adv1.":::

1. Sélectionnez **Enregistrer**.

#### <a name="microsoft-azure-active-directory-azure-ad-v2"></a>Prise en charge de CORS dans Microsoft Azure Active Directory (Azure AD) V2

1. Dans le [**Portail Azure**][azure-portal], sélectionnez votre bot Azure dans le tableau de bord.
1. Dans la page de ressources, sélectionnez **Configuration** sous **Paramètres**.
1. Sélectionnez le bouton **Ajouter des paramètres de connexion OAuth** sur l’écran Configuration.  
   L’image suivante affiche la sélection correspondante dans la page de ressources :

   :::image type="content" source="../../../assets/images/authentication/sample-app-demo-bot-configuration.png" alt-text="Cette capture d’écran montre la sélection correspondante dans la page de ressources.":::

1. Remplissez le formulaire comme suit :

    1. **Nom**. Entrez un nom descriptif pour la connexion. Vous allez utiliser ce nom dans votre bot dans le `appsettings.json` fichier. Par exemple, *BotTeamsAuthADv2*.
    1. **Fournisseur de services** Sélectionnez **Microsoft Azure Active Directory v2**. Une fois que vous sélectionnez cette option, les champs spécifiques à Azure AD s’affichent.
    1. **ID client**. Entrez l’ID d’application (client) que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.
    1. **Clé secrète client** Entrez le secret que vous avez enregistré pour votre application de fournisseur d’identité Azure dans les étapes ci-dessus.
    1. Jeton **URL Exchange** Laissez ce champ vide.
    1. **ID de locataire**, entrez **l’ID d’annuaire (locataire)** que vous avez enregistré précédemment pour votre application d’identité Azure ou **commun** en fonction du type de compte pris en charge sélectionné lors de la création de l’application de fournisseur d’identité. Pour déterminer la valeur à attribuer, suivez les critères suivants :

        - Si vous avez sélectionné *comptes uniquement dans cet annuaire organisationnel (Microsoft uniquement - Locataire unique)* ou *Comptes dans un annuaire organisationnel (Microsoft Azure Active Directory - Multilocataire),* entrez **l’ID de locataire** que vous avez enregistré précédemment pour l’application Azure AD. Il s’agit du locataire associé aux utilisateurs qui peuvent être authentifiés.

        - Si vous avez sélectionné *Comptes dans un annuaire organisationnel (Tout Microsoft Azure Active Directory (Azure AD) - Comptes Microsoft multilocataires et personnels, par exemple, Skype, Xbox, Outlook)* entrez le mot **commun** au lieu d’un ID de locataire. Sinon, l’application Azure AD vérifie par le biais du locataire dont l’ID a été sélectionné et exclut les comptes Microsoft personnels.

    1. Pour **les étendues**, entrez une liste délimitée par des espaces des autorisations de graphe requises par cette application, par exemple : User.Read User.ReadBasic.All Mail.Read

1. Sélectionnez **Enregistrer**.

### <a name="test-the-connection"></a>Tester la connexion

1. Sélectionnez l’entrée de connexion pour ouvrir la connexion que vous avez créée.
1. Sélectionnez **Tester la connexion** en haut du panneau **Paramètres de connexion du fournisseur de** services.
1. La première fois que vous effectuez cette opération, une nouvelle fenêtre de navigateur s’ouvre pour vous demander de sélectionner un compte. Sélectionnez le sous-réseau que vous souhaitez utiliser.
1. Ensuite, vous serez invité à autoriser le fournisseur d’identité à utiliser vos données (informations d’identification). L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-accept.PNG" alt-text="La capture d’écran montre comment ajouter la chaîne de connexion d’authentification du bot Teams adv1.":::

1. Sélectionnez **Accepter**.
1. Cela doit ensuite vous rediriger vers une **connexion de test vers la page \<your-connection-name>Réussite** . Actualisez la page si vous obtenez une erreur. L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-token.PNG" alt-text="La capture d’écran montre comment ajouter la chaîne de connexion d’authentification de l’application Teams adv1.":::

Le nom de connexion est utilisé par le code du bot pour récupérer les jetons d’authentification utilisateur.

## <a name="prepare-the-bot-sample-code"></a>Préparer l’exemple de code du bot

Une fois les paramètres préliminaires terminés, concentrons-nous sur la création du bot à utiliser dans cet article.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. Cloner [cs-auth-sample][teams-auth-bot-cs]
1. Lancez Visual Studio.
1. Dans la barre d’outils, sélectionnez **Fichier -> Ouvrir -> Projet/Solution** et ouvrez le projet de bot.
1. En C#, mettez à jour **appsettings.json** comme suit :

    - Définissez `ConnectionName` le nom de la connexion du fournisseur d’identité que vous avez ajoutée à l’inscription du bot. Le nom que nous avons utilisé dans cet exemple est *BotTeamsAuthADv1*.
    - Définissez `MicrosoftAppId` l’ID d’application **du bot** que vous avez enregistré au moment de l’inscription du bot.
    - Définissez `MicrosoftAppPassword` la **clé secrète client** que vous avez enregistrée au moment de l’inscription du bot.

    Selon les caractères de votre secret de bot, vous devrez peut-être placer le mot de passe dans un échappement XML. Par exemple, tous les ampersands (&) doivent être encodés en tant que `&amp;`.

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. Dans le Explorateur de solutions, accédez au `TeamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id` et `botId` accédez à **l’ID d’application du bot** que vous avez enregistré au moment de l’inscription du bot.

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. [Cloner node-auth-sample][teams-auth-bot-js].
1. Dans une console, accédez au projet : </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. Installer les modules</br></br>
`npm install`
1. Mettez à jour la configuration **de .env** comme suit :

    - Définissez `MicrosoftAppId` l’ID d’application **du bot** que vous avez enregistré au moment de l’inscription du bot.
    - Définissez `MicrosoftAppPassword` la **clé secrète client** que vous avez enregistrée au moment de l’inscription du bot.
    - Définissez le `connectionName` nom de la connexion du fournisseur d’identité.
    Selon les caractères de votre secret de bot, vous devrez peut-être placer le mot de passe dans un échappement XML. Par exemple, tous les ampersands (&) doivent être encodés en tant que `&amp;`.

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. Dans le `teamsAppManifest` dossier, ouvrez `manifest.json` et définissez `id`  votre **ID d’application Microsoft** et `botId` **l’ID d’application du bot** que vous avez enregistré au moment de l’inscription du bot.

# <a name="python"></a>[Python](#tab/python)

1. Clonez [py-auth-sample][teams-auth-bot-py] à partir du référentiel github.
1. Mettre à jour **config.py** :

    - Définissez `ConnectionName` le nom du paramètre de connexion OAuth que vous avez ajouté à votre bot.
    - Définissez et `MicrosoftAppPassword` définissez `MicrosoftAppId` l’ID d’application et le secret d’application de votre bot.

      Selon les caractères de votre secret de bot, vous devrez peut-être placer le mot de passe dans un échappement XML. Par exemple, tous les ampersands (&) doivent être encodés en tant que `&amp;`.

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Déployer le bot sur Azure

Pour déployer le bot, suivez les étapes de la procédure de [déploiement de votre bot sur Azure](https://aka.ms/azure-bot-deployment-cli).

Dans Visual Studio, vous pouvez également effectuer les étapes suivantes :

1. Dans Visual Studio *Explorateur de solutions*, sélectionnez et maintenez le nom du projet enfoncé (ou cliquez avec le bouton droit).
1. Dans le menu déroulant qui apparaît, sélectionner **Publier**.
1. Dans la fenêtre affichée, sélectionnez le **nouveau** lien.
1. Dans la fenêtre de dialogue, sélectionnez **App Service** sur la gauche et **Créer nouveau** à droite.
1. Sélectionnez le bouton **Publier**.
1. Dans la fenêtre de dialogue suivante, entrez les informations requises. Voici un exemple :

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service.png" alt-text="Cette capture d’écran montre comment entrer les informations requises pour auth app service.":::

1. Sélectionnez **Créer**.
1. Si le déploiement se termine correctement, vous devriez le voir reflété dans Visual Studio. En outre, une page s’affiche dans votre navigateur par défaut indiquant que *votre bot est prêt!*. L'URL ressemble à ceci :`https://botteamsauth.azurewebsites.net/`. Enregistrez-le dans un fichier.
1. Dans votre navigateur, accédez au [**portail Azure**][azure-portal] et connectez-vous.
1. Vérifiez votre groupe de ressources. Le bot doit être répertorié avec les autres ressources. L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service-in-group.png" alt-text="Cette capture d’écran montre comment vérifier le groupe de ressources et le bot.":::

1. Dans le groupe de ressources, sélectionnez le nom d’inscription du bot (lien).
1. Dans le panneau gauche, sélectionnez **Paramètres**
1. Dans la zone **de point de terminaison de messagerie** , entrez l’URL obtenue ci-dessus, suivie de `api/messages`. Voici un exemple : `https://botteamsauth.azurewebsites.net/api/messages`.
    > [!NOTE]
    > Un seul point de terminaison de messagerie est autorisé pour un bot.
1. Sélectionnez le bouton **Enregistrer** dans le coin supérieur gauche.

## <a name="test-the-bot-using-the-emulator"></a>Tester le bot à l’aide de la Emulator

Si vous ne l’avez pas déjà fait, installez le [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme). Voir aussi [Déboguer avec le Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator)

Pour que l’exemple de connexion du bot fonctionne, vous devez configurer le Emulator.

### <a name="configure-the-emulator-for-authentication"></a>Configurer le Emulator pour l’authentification

Si un bot nécessite une authentification, vous devez configurer le Emulator. Pour configurer :

1. Démarrez le Emulator.
1. Dans le Emulator, sélectionnez l’icône d’engrenage &#9881; en bas à gauche ou l’onglet **Paramètres Emulator** dans le coin supérieur droit.
1. Cochez la case **en utilisant les jetons d’authentification version 1.0**.
1. Entrez le chemin local de l’outil **ngrok** . *Consultez* le [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)) d’intégration du tunneling Bot Framework Emulator/ngrok. Pour plus d’informations sur les outils, consultez [ngrok](https://ngrok.com/).
1. Cochez la case en **exécutant ngrok lorsque le Emulator démarre**.
1. Sélectionnez le bouton **Enregistrer** .

Lorsque le bot affiche une carte de connexion et que l’utilisateur sélectionne le bouton de connexion, le Emulator ouvre une page que l’utilisateur peut utiliser pour se connecter avec le fournisseur d’authentification.
Une fois que l’utilisateur le fait, le fournisseur génère un jeton utilisateur et l’envoie au bot. Après cela, le bot peut agir pour le compte de l’utilisateur.

### <a name="test-the-bot-locally"></a>Tester le bot de conversation

Une fois que vous avez configuré le mécanisme d’authentification, vous pouvez effectuer le test de bot réel.  

1. Exécutez l’exemple de bot localement sur votre ordinateur, par exemple via Visual Studio.
1. Démarrez le Emulator.
1. Sélectionnez le bouton **Ouvrir le bot** .
1. Dans **l’URL** du bot, entrez l’URL locale du bot. Généralement dans `http://localhost:3978/api/messages`
1. Dans **l’ID d’application Microsoft** , entrez l’ID d’application du bot à partir de `appsettings.json`.
1. Dans le **mot de passe de l’application Microsoft** , entrez le mot de passe de l’application `appsettings.json`du bot à partir du .
1. Sélectionnez **Connexion**.
1. Une fois le bot opérationnel, entrez un texte pour afficher la carte de connexion.
1. Sélectionnez le bouton **Se connecter**.
1. Une boîte de dialogue contextuelle s’affiche pour **confirmer l’URL d’ouverture**. Cela permet à l’utilisateur du bot (vous) d’être authentifié.  
1. Sélectionner **Confirmer**.
1. Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.
1. Selon la configuration que vous avez utilisée pour le Emulator, vous obtenez l’une des options suivantes :
    1. **Utilisation du code de vérification de connexion**  
      &#x2713; Une fenêtre s’ouvre et affiche le code de validation.  
      &#x2713; copier et entrer le code de validation dans la zone de conversation pour terminer la connexion
    1. **Utilisation de jetons d’authentification**  
      &#x2713; Vous êtes connecté en fonction de vos informations d’identification.

    L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :

    :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator.PNG" alt-text="Cette capture d’écran montre un exemple de l’interface utilisateur du bot après vous être connecté.":::

1. Si vous sélectionnez **Oui** lorsque le bot vous demande *Voulez-vous afficher votre jeton ?* Vous obtiendrez une réponse similaire à ce qui suit :

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator-token.png" alt-text="Cette capture d’écran montre comment sélectionner le consentement.":::

1. Entrez **la déconnexion** dans la zone de conversation d’entrée pour vous déconnecter. Cela libère le jeton utilisateur, et le bot ne pourra pas agir en votre nom tant que vous ne vous reconnectez pas.

> [!NOTE]
> L’authentification de bot nécessite l’utilisation du **service Bot Connector**. Le service accède aux informations d’inscription des bots pour votre bot.

## <a name="test-the-deployed-bot"></a>Tester le bot de conversation

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. Dans votre navigateur, accédez au [**portail Azure**][azure-portal] et connectez-vous.
1. Recherchez votre groupe de ressources.
1. Sélectionnez le lien de ressource. La page de ressource s’affiche.
1. Dans la page de ressources, sélectionnez **Tester dans Chat Web**. Le bot démarre et affiche les salutations prédéfinies.
1. Tapez n’importe quoi dans la zone de conversation.
1. Sélectionnez la zone **Connexion** .
1. Une boîte de dialogue contextuelle s’affiche pour **confirmer l’URL d’ouverture**. Cela permet à l’utilisateur du bot (vous) d’être authentifié.  
1. Sélectionner **Confirmer**.
1. Si vous y êtes invité, sélectionnez le compte de l’utilisateur applicable.
    L’image suivante est un exemple de l’interface utilisateur du bot après vous être connecté :

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed.PNG" alt-text="Cette capture d’écran montre un exemple de l’interface utilisateur du bot Teams après vous être connecté.":::

1. Sélectionnez le bouton **Oui** pour afficher votre jeton d’authentification. L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed-token.PNG" alt-text="Cette capture d’écran montre comment sélectionner le bouton Oui pour afficher votre jeton d’authentification.":::

1. Entrez la déconnexion pour vous déconnecter.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-deployed-logout.PNG" alt-text="Cette capture d’écran montre comment entrer la déconnexion pour se déconnecter.":::

> [!NOTE]
> Si vous rencontrez des problèmes de connexion, essayez de tester à nouveau la connexion comme décrit dans les étapes précédentes. Cela peut recréer le jeton d’authentification.
> Avec le client Bot Framework Chat Web dans Azure, vous devrez peut-être vous connecter plusieurs fois avant d’établir correctement l’authentification.

## <a name="install-and-test-the-bot-in-teams"></a>Installer et tester le bot dans Teams

1. Dans votre projet de bot, assurez-vous que le `TeamsAppManifest` dossier contient les `manifest.json` fichiers et `color.png` les `outline.png` fichiers.
1. Dans l'explorateur de solutions, naviguez jusqu'au dossier `TeamsAppManifest`. Modifiez `manifest.json` en affectant les valeurs suivantes :
    1. Vérifiez que **l’ID d’application de bot** que vous avez reçu au moment de l’inscription du bot est affecté `id` et `botId`.
    1. Affectez cette valeur : `validDomains: [ "token.botframework.com" ]`.
1. Sélectionnez et **compressez** les fichiers, `manifest.json`et `outline.png` les `color.png`fichiers.
1. Ouvrez **Microsoft Teams**.
1. Dans le volet gauche, en bas, sélectionnez **l’icône Applications**.
1. Dans le volet droit, en bas, sélectionnez **Télécharger une application personnalisée**.
1. Accédez au `TeamsAppManifest` dossier et chargez le manifeste compressé.
L’assistant de l’importation de tâche s’affiche.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-upload.png" alt-text="Cette capture d’écran montre un exemple du bot après son chargement dans Teams.":::

1. Sélectionnez le bouton **Ajouter à une équipe**.
1. Dans la fenêtre suivante, sélectionnez l’équipe dans laquelle vous souhaitez utiliser le bot.
1. Sélectionnez le bouton **Configurer un bot** .
1. Sélectionnez les trois points (&#x25cf;&#x25cf;&#x25cf;) dans le volet gauche. Sélectionnez ensuite l’icône **Portail des développeurs** .
1. Sélectionnez l’onglet **Éditeur de manifeste** . L’icône du bot que vous avez chargé doit s’afficher.
1. En outre, vous devriez être en mesure de voir le bot répertorié en tant que contact dans la liste de conversation que vous pouvez utiliser pour échanger des messages avec le bot.

### <a name="testing-the-bot-locally-in-teams"></a>Test du bot localement dans Teams

Teams est un produit entièrement basé sur le cloud. Tous les services accessibles doivent être disponibles à partir du cloud à l’aide de points de terminaison HTTPS. Par conséquent, pour permettre au bot (notre exemple) de fonctionner dans Teams, vous devez soit publier le code dans le cloud de votre choix, soit rendre une instance en cours d’exécution localement accessible en externe via un outil **de tunneling**. Nous vous recommandons  [ngrok](https://ngrok.com/download), qui crée une URL adressable en externe pour un port que vous ouvrez localement sur votre ordinateur.
Pour configurer ngrok en vue de l’exécution locale de votre application Teams, procédez comme suit :

1. Dans une fenêtre de terminal, accédez au répertoire où vous avez `ngrok.exe` installé. Nous vous suggérons de définir le chemin de *la variable d’environnement* pour qu’il pointe vers celui-ci.
1. Exécutez, par exemple, `ngrok http 3978 --host-header=localhost:3978`. Remplacez le numéro de port en fonction des besoins.
Cela lance ngrok pour écouter sur le port que vous spécifiez. En retour, il vous donne une URL adressable en externe, valide tant que ngrok est en cours d’exécution. L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-ngrok-start.PNG" alt-text="Cette capture d’écran montre la chaîne de connexion d’authentification de l’application bot Teams adv1":::

1. Copiez l’adresse HTTPS de transfert. Il doit se présenter comme suit :`https://dea822bf.ngrok.io/`.
1. `/api/messages` Ajouter pour obtenir `https://dea822bf.ngrok.io/api/messages` Il s’agit du **point de terminaison des messages** pour le bot s’exécutant localement sur votre ordinateur et accessible sur le web dans une conversation dans Teams.
1. Une dernière étape à effectuer consiste à mettre à jour le point de terminaison des messages du bot déployé. Dans l’exemple, nous avons déployé le bot dans Azure. Procédons donc comme suit :
    1. Dans votre navigateur, accédez au [**portail Azure**][azure-portal] et connectez-vous.
    1. Sélectionnez votre **inscription de bot**.
    1. Dans le panneau gauche, sélectionnez **Paramètres**
    1. Dans le volet droit, dans la zone de point **de terminaison de messagerie**, entrez l’URL ngrok, dans notre exemple. `https://dea822bf.ngrok.io/api/messages`
1. Démarrez votre bot localement, par exemple en mode de débogage Visual Studio.
1. Testez le bot en cours d’exécution localement à l’aide de la **conversation web test** du portail Bot Framework. Comme le Emulator, ce test ne vous permet pas d’accéder à Teams fonctionnalité spécifique.
1. Dans la fenêtre de terminal où `ngrok` s’exécute l’exécution, vous pouvez voir le trafic HTTP entre le bot et le client de conversation web. Si vous souhaitez obtenir une vue plus détaillée, dans une fenêtre de navigateur, entrez `http://127.0.0.1:4040` ce que vous avez obtenu à partir de la fenêtre de terminal précédente. L’image suivante est un exemple.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png" alt-text="Cette capture d’écran montre les tests ngrok des équipes de bot d’authentification.":::

> [!NOTE]
> Si vous arrêtez et redémarrez ngrok, l’URL change. Pour utiliser ngrok dans votre projet, et en fonction des fonctionnalités que vous utilisez, vous devez mettre à jour toutes les références d’URL.

## <a name="additional-information"></a>Informations supplémentaires

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.json

Ce manifeste contient les informations nécessaires à Teams pour se connecter au bot :  

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

### <a name="handling-invoke-activity"></a>Gestion de l’activité Invoke

Une **activité invoke** est envoyée au bot plutôt qu’à l’activité d’événement utilisée par d’autres canaux.
Pour ce faire, sous-classez **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

*L’activité Invoke* doit être transférée vers la boîte de dialogue si **OAuthPrompt** est utilisé.

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

*L’activité Invoke* doit être transférée vers la boîte de dialogue si **OAuthPrompt** est utilisé.

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**dialogues/mainDialog.js**

Dans une étape de dialogue, utilisez `beginDialog` cette option pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.

- Si l’utilisateur est déjà connecté, cela génère un événement de réponse de jeton, sans inviter l’utilisateur.
- Dans le cas contraire, l’utilisateur est invité à se connecter. Azure Bot Service envoie l’événement de réponse de jeton après que l’utilisateur a tenté de se connecter.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente. S’il n’est pas null, l’utilisateur s’est connecté avec succès.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

*L’activité Invoke* doit être transférée vers la boîte de dialogue si **OAuthPrompt** est utilisé.

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogs/main_dialog.py**

Dans une étape de dialogue, utilisez `begin_dialog` cette option pour démarrer l’invite OAuth, qui demande à l’utilisateur de se connecter.

- Si l’utilisateur est déjà connecté, cela génère un événement de réponse de jeton, sans inviter l’utilisateur.
- Dans le cas contraire, l’utilisateur est invité à se connecter. Azure Bot Service envoie l’événement de réponse de jeton après que l’utilisateur a tenté de se connecter.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

Dans l’étape de dialogue suivante, vérifiez la présence d’un jeton dans le résultat de l’étape précédente. S’il n’est pas null, l’utilisateur s’est connecté avec succès.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogs/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="code-sample"></a>Exemple de code

Cette section fournit un exemple de Kit de développement logiciel (SDK) d’authentification de bot v3.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Authentification du bot | Cet exemple montre comment commencer à utiliser l’authentification dans un bot pour Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Authentification unique Tab, Bot and Message Extension (ME) | Cet exemple montre l’authentification unique pour Tab, Bot et ME – recherche, action, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | Non disponible |

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
