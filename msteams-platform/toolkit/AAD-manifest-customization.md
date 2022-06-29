---
title: Gérer l’application Azure Active Directory dans le Kit de ressources Teams
author: zyxiaoyuer
description: Décrit la gestion de l’application Azure Active Directory dans le Kit de ressources Teams
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 1f71d57e32bd6fb24cf75cc6027937337f29f972
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503787"
---
# <a name="customize-azure-ad-manifest"></a>Personnaliser le manifeste Azure AD

Le [manifeste Azure Active Directory (Azure AD)](/azure/active-directory/develop/reference-app-manifest) contient des définitions de tous les attributs d’un objet d’application Azure AD dans le Plateforme d'identités Microsoft.

Teams Toolkit gère désormais l’application Azure AD avec le fichier manifeste comme source de vérité pendant vos cycles de vie de développement d’applications Teams.

## <a name="customize-azure-ad-manifest-template"></a>Personnaliser le modèle de manifeste Azure AD

Vous pouvez personnaliser le modèle de manifeste Azure AD pour mettre à jour l’application Azure AD.

1. Ouvrez `aad.template.json` votre projet.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. Mettez à jour le modèle directement ou [référencez les valeurs d’un autre fichier](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template). Vous pouvez voir plusieurs scénarios de personnalisation ici :
  
   * [Ajouter une autorisation d’application](#customize-requiredresourceaccess)
   * [Préauthoriser une application cliente](#customize-preauthorizedapplications)
   * [Mettre à jour l’URL de redirection pour la réponse d’authentification](#customize-redirect-urls)

3. [Déployez les modifications d’application Azure AD pour l’environnement local](#deploy-azure-ad-application-changes-for-local-environment).
  
4. [Déployez les modifications apportées à l’application Azure AD pour l’environnement distant](#deploy-azure-ad-application-changes-for-remote-environment).

### <a name="customize-requiredresourceaccess"></a>Personnaliser requiredResourceAccess

Si l’application Teams nécessite plus d’autorisations pour appeler l’API avec des autorisations supplémentaires, vous devez mettre à jour `requiredResourceAccess` la propriété dans le modèle de manifeste Azure AD. Vous pouvez voir l’exemple suivant pour cette propriété :

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId` est pour différentes API, pour `Microsoft Graph` et `Office 365` `SharePoint Online`, entrez le nom directement à la place de l’UUID, et pour d’autres API, utilisez L’UUID.

* `resourceAccess.id` est pour différentes autorisations, pour `Microsoft Graph` et `Office 365 SharePoint Online`, entrez le nom d’autorisation directement au lieu de l’UUID, et pour d’autres API, utilisez UUID.

* `resourceAccess.type` est utilisée pour l’autorisation déléguée ou l’autorisation d’application. `Scope` signifie l’autorisation déléguée et `Role` l’autorisation d’application.

### <a name="customize-preauthorizedapplications"></a>Personnaliser les préAuthorizedApplications

Vous pouvez utiliser `preAuthorizedApplications` la propriété pour autoriser une application cliente à indiquer que l’API approuve l’application et que les utilisateurs ne consentent pas lorsque le client l’appelle API exposée. Vous pouvez voir l’exemple suivant pour cette propriété :

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` est utilisée pour l’application que vous souhaitez autoriser. Si vous ne connaissez pas l’ID d’application, mais que vous ne connaissez que le nom de l’application, vous pouvez accéder à Portail Azure et suivre les étapes pour rechercher l’ID dans l’application :

1. Accédez à [Portail Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) et ouvrez les inscriptions d’applications.

1. Sélectionnez **Toutes les applications** et recherchez le nom de l’application.

1. Sélectionnez le nom de l’application et obtenez l’ID d’application à partir de la page de vue d’ensemble.

### <a name="customize-redirect-urls"></a>Personnaliser les URL de redirection

  Les URL de redirection sont utilisées lors du retour de réponses d’authentification telles que des jetons après une authentification réussie. Vous pouvez personnaliser les URL de redirection à l’aide de la propriété `replyUrlsWithType`, par exemple, pour l’ajouter `https://www.examples.com/auth-end.html` en tant qu’URL de redirection, vous pouvez l’ajouter comme exemple suivant :

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## <a name="azure-ad-manifest-template-placeholders"></a>Espaces réservés de modèle de manifeste Azure AD

Le fichier manifeste Azure AD contient des arguments d’espace réservé avec {{...}} instructions qu’il est remplacé pendant la génération pour différents environnements. Vous pouvez créer des références aux variables de fichier de configuration, de fichier d’état et d’environnement avec les arguments d’espace réservé.

### <a name="reference-state-file-values-in-azure-ad-manifest-template"></a>Référencer les valeurs de fichier d’état dans le modèle de manifeste Azure AD

Le fichier d’état se trouve dans `.fx\states\state.xxx.json` (xxx représente un environnement différent). L’exemple suivant montre un fichier d’état classique :

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

Vous pouvez utiliser cet argument d’espace réservé dans le manifeste Azure AD : `{{state.fx-resource-aad-app-for-teams.applicationIdUris}}` pour référencer `applicationIdUris` la valeur dans la `fx-resource-aad-app-for-teams` propriété.

### <a name="reference-config-file-values-in-azure-ad-manifest-template"></a>Référencer les valeurs de fichier de configuration dans le modèle de manifeste Azure AD

Le fichier config se trouve dans `.fx\configs\config.xxx.json` (xxx représente un environnement différent). L’exemple suivant montre le fichier de configuration :

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

Vous pouvez utiliser l’argument espace réservé dans le manifeste Azure AD : `{{config.manifest.appName.short}}` pour référencer `short` la valeur.

### <a name="reference-environment-variable-in-azure-ad-manifest-template"></a>Variable d’environnement de référence dans le modèle de manifeste Azure AD

Parfois, vous ne souhaitez pas coder en dur les valeurs dans le modèle de manifeste Azure AD. Par exemple, lorsque la valeur est un secret. Le fichier de modèle de manifeste Azure AD prend en charge les valeurs des variables d’environnement de référence. Vous pouvez utiliser la syntaxe `{{env.YOUR_ENV_VARIABLE_NAME}}` dans les valeurs de paramètre pour indiquer aux outils de résoudre la variable d’environnement actuelle de valeur.

## <a name="author-and-preview-azure-ad-manifest-with-code-lens"></a>Créer et afficher un aperçu du manifeste Azure AD avec objectif de code

Le fichier de modèle de manifeste Azure AD a une lentille de code à examiner et à modifier.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="previewview":::

### <a name="azure-ad-manifest-template-file"></a>Fichier de modèle de manifeste Azure AD

Au début du fichier de modèle de manifeste Azure AD, il existe une lentille de code en préversion. Sélectionnez l’objectif de code. Il génère le manifeste Azure AD en fonction de l’environnement que vous avez sélectionné.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>Objectif de code d’argument d’espace réservé

L’objectif de code d’argument d’espace réservé vous permet d’examiner rapidement les valeurs pour le débogage local et de développer l’environnement. Si votre souris pointe sur l’argument espace réservé, elle affiche la zone d’info-bulle pour les valeurs de tout l’environnement.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>Objectif de code d’accès aux ressources requis

Il est différent du schéma de [manifeste Azure AD](/azure/active-directory/develop/reference-app-manifest) officiel qui `resourceAppId` et `resourceAccess` l’ID dans la propriété prend uniquement en `requiredResourceAccess` charge l’UUID, le modèle de manifeste Azure AD dans Teams Toolkit prend également en charge les chaînes lisibles par l’utilisateur et `Microsoft Graph` `Office 365 SharePoint Online` les autorisations. Si vous entrez UUID, l’objectif de code affiche les chaînes lisibles par l’utilisateur; sinon, il affiche l’UUID.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### <a name="pre-authorized-applications-code-lens"></a>Objectif de code des applications pré-autorisées

L’objectif de code affiche le nom de l’application pour l’ID d’application par autorisation pour la `preAuthorizedApplications` propriété.

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>Déployer les modifications apportées aux applications Azure AD pour l’environnement local

1. Sélectionnez `Preview` l’objectif de code dans `aad.template.json`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. Sélectionnez `local` l’environnement.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. Sélectionnez `Deploy Azure AD Manifest` l’objectif de code dans `aad.local.json`.

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. Les modifications apportées à l’application Azure AD utilisée dans l’environnement local sont déployées.
  
## <a name="deploy-azure-ad-application-changes-for-remote-environment"></a>Déployer des modifications d’application Azure AD pour l’environnement distant

1. Ouvrez la palette de commandes et sélectionnez : `Teams: Deploy Azure Active Directory application manifest`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. Vous pouvez également cliquer avec le bouton droit sur le `aad.template.json` menu contextuel et le sélectionner `Deploy Azure Active Directory application manifest` .
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## <a name="view-azure-ad-application-on-the-azure-portal"></a>Afficher l’application Azure AD sur le Portail Azure

1. Copiez l’ID client de l’application Azure AD à partir du `state.xxx.json` fichier (xxx est le nom de l’environnement dans lequel vous avez déployé l’application Azure AD) dans la `fx-resource-aad-app-for-teams` propriété.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

2. Accédez à [Portail Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) et connectez-vous au compte Microsoft 365.
  
   > [!NOTE]
   > Vérifiez que les informations d’identification de connexion de l’application Teams et du compte M365 sont identiques.

3. Ouvrez la [page Inscriptions d’applications](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), recherchez l’application Azure AD à l’aide de l’ID client que vous avez copié précédemment.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. Sélectionnez l’application Azure AD dans le résultat de la recherche pour afficher les informations détaillées.
  
5. Dans la page d’informations de l’application Azure AD, sélectionnez le `Manifest` menu pour afficher le manifeste de cette application. Le schéma du manifeste est identique à celui du `aad.template.json` fichier. Pour plus d’informations sur le manifeste, consultez le [manifeste de l’application Azure Active Directory](/azure/active-directory/develop/reference-app-manifest).
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. Vous pouvez sélectionner **Autre menu** pour afficher ou configurer l’application Azure AD via le portail.
  
## <a name="use-an-existing-azure-ad-application"></a>Utiliser une application Azure AD existante

Vous pouvez utiliser l’application Azure AD existante pour le projet Teams. Pour plus d’informations, consultez [Utiliser une application Azure AD existante pour votre application Teams](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app).

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Cycle de vie du développement d’applications Azure AD dans Teams

Vous devez interagir avec l’application Azure AD pendant différentes étapes du cycle de vie de développement de votre application Teams.

1. **Pour créer un projet**

      Vous pouvez créer un projet avec le Kit de ressources Teams fourni avec la prise en charge de l’authentification unique par défaut, par `SSO-enabled tab`exemple . Pour plus d’informations sur la création d’une application, consultez [créer une application Teams à l’aide du Kit de ressources Teams](create-new-project.md). Un fichier manifeste Azure AD est automatiquement créé pour vous : `templates\appPackage\aad.template.json`. Teams Toolkit crée ou met à jour l’application Azure AD pendant le développement local ou pendant que vous déplacez l’application vers le cloud.

2. **Pour ajouter l’authentification unique à votre bot ou onglet**

      Une fois que vous avez créé une application Teams sans authentification unique intégrée, Teams Toolkit vous aide de façon incrémentielle à ajouter l’authentification unique pour le projet. Par conséquent, un fichier manifeste Azure AD est automatiquement créé pour vous : `templates\appPackage\aad.template.json`.

      Teams Toolkit crée ou met à jour l’application Azure AD lors de la session de débogage locale suivante ou pendant que vous déplacez l’application vers le cloud.

3. **Pour générer localement**

    Teams Toolkit exécute les fonctions suivantes pendant le développement local (appelé F5) :

    * Lisez le `state.local.json` fichier pour trouver une application Azure AD existante. S’il existe déjà une application Azure AD, teams Toolkit réutilise l’application Azure AD existante, sinon vous devez créer une application à l’aide du `aad.template.json` fichier.

    * Ignore initialement certaines propriétés du fichier manifeste qui nécessitent un contexte supplémentaire (comme la propriété replyUrls qui nécessite un point de terminaison de débogage local) lors de la création d’une application Azure AD avec le fichier manifeste.

    * Une fois le démarrage de l’environnement de développement local réussi, les identificateurs, les replyUrls et d’autres propriétés de l’application Azure AD qui ne sont pas disponibles pendant l’étape de création sont mis à jour en conséquence.

    * Les modifications que vous avez apportées à votre application Azure AD sont chargées lors de la prochaine session de débogage locale. Vous pouvez voir [les modifications apportées à l’application Azure AD](https://github.com/OfficeDev/TeamsFx/wiki/) pour appliquer manuellement les modifications apportées à l’application Azure AD.

4. **Pour provisionner des ressources cloud**

      Vous devez provisionner des ressources cloud et déployer votre application tout en déplaçant votre application vers le cloud. Au niveau des étapes, comme le développement local, Teams Toolkit :

      * Lisez le `state.{env}.json` fichier pour trouver une application Azure AD existante. S’il existe déjà une application Azure AD, teams Toolkit réutilise l’application Azure AD existante, sinon vous devez créer une application à l’aide du `aad.template.json` fichier.

      * Ignore initialement certaines propriétés du fichier manifeste qui nécessitent un contexte supplémentaire (par exemple, la propriété replyUrls nécessite un point de terminaison de serveur frontal ou de bot) lors de la création d’une application Azure AD avec le fichier manifeste.

      * Une fois l’approvisionnement d’autres ressources terminé, les identificateurs d’application Azure AD et replyUrls sont mis à jour en conséquence pour les points de terminaison appropriés.

5. **Pour générer une application**

    * La commande Déployer dans le cloud déploie votre application sur les ressources approvisionnées. Il n’inclut pas le déploiement des modifications apportées à l’application Azure AD.

    * Vous pouvez voir, [Déployer les modifications d’application Azure AD pour l’environnement distant](#deploy-azure-ad-application-changes-for-remote-environment) afin de déployer des modifications d’application Azure AD pour l’environnement distant.

    * Teams Toolkit met à jour l’application Azure AD en fonction du fichier de modèle de manifeste Azure AD.

## <a name="limitations"></a>Limites

1. L’extension Teams Toolkit ne prend pas en charge toutes les propriétés répertoriées dans le schéma de manifeste Azure AD.
  
      Le tableau suivant répertorie les propriétés qui ne sont pas prises en charge dans l’extension Teams Toolkit :

      |**Propriétés non prises en charge**|**Raison**|
      |-----------|----------|
      |passwordCredentials|Non autorisé dans le manifeste|
      |createdDateTime|Lecture seule et ne peut pas changer|
      |logoUrl|Lecture seule et ne peut pas changer|
      |publisherDomain|Lecture seule et ne peut pas changer|
      |oauth2RequirePostResponse|N’existe pas dans API Graph|
      |oauth2AllowUrlPathMatching|N’existe pas dans API Graph|
      |samlMetadataUrl|N’existe pas dans API Graph|
      |orgRestrictions|N’existe pas dans API Graph|
      |certification|N’existe pas dans API Graph|

2. Actuellement, `requiredResourceAccess` la propriété peut utiliser le nom de l’application de ressource lisible par l’utilisateur ou les chaînes de nom d’autorisation uniquement pour `Microsoft Graph` et `Office 365 SharePoint Online` les API. Pour les autres API, vous devez utiliser l’UUID à la place. Vous pouvez suivre ces étapes pour récupérer des ID à partir de Portail Azure :

    * Inscrivez une nouvelle application Azure AD sur [Portail Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
    * Sélectionnez dans `API permissions` la page de l’application Azure AD.
    * Sélectionnez `add a permission` cette option pour ajouter l’autorisation souhaitée.
    * Sélectionnez `Manifest`, dans la `requiredResourceAccess` propriété, les ID d’API et d’autorisations.

## <a name="see-also"></a>Voir aussi

* [Afficher un aperçu et personnaliser le manifeste de l’application dans le Kit de ressources](TeamsFx-preview-and-customize-app-manifest.md)
