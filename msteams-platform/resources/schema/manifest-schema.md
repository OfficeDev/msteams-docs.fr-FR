---
title: Référence du schéma de manifeste
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: schéma de manifeste teams
ms.openlocfilehash: 061b39430cf8eba229b4e0c3012a5bbf752a5e85
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801373"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Référence : schéma de manifeste pour Microsoft teams

Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams. Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) . Les versions précédentes 1.0 à 1.4 sont également prises en charge (à l’aide de « v1. x » dans l’URL).

L’exemple de schéma suivant montre toutes les options d’extensibilité.

## <a name="sample-full-manifest"></a>Exemple de manifeste complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "query",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        }
      ],
      "messageHandlers": [
        {
          "type" : "link",
          "value" : {
            "domains" : [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

*Facultatif, mais recommandé* &ndash; Chaîne

URL https://référençant le schéma JSON du manifeste.

## <a name="manifestversion"></a>manifestVersion

**Obligatoire** &ndash; Chaîne

Version du schéma de manifeste utilisé par ce manifeste. Il doit être « 1,5 ».

## <a name="version"></a>version

**Obligatoire** &ndash; Chaîne

Version de l’application spécifique. Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée. Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités. Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé. Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.

Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.

Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).

## <a name="id"></a>id

**Obligatoire** &ndash; ID de l’application Microsoft

Identificateur unique généré par Microsoft pour cette application. Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici. Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez un bot. Remarque : Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.

## <a name="packagename"></a>packageName

**Obligatoire** &ndash; Chaîne

Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.

## <a name="developer"></a>developer

**Obligatoire**

Spécifie les informations relatives à votre société. Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource. Pour plus d’informations, consultez nos [instructions de publication](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) .

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔|URL https://vers le site Web du développeur. Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.|
|`privacyUrl`|2 048 caractères|✔|URL https://vers la stratégie de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|L’URL https://vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères| |**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires. Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant des traductions de langue supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`||✔|Balise de langue des chaînes dans le fichier fourni.|
|`file`||✔|Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.|

## <a name="name"></a>name

**Obligatoire**

Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource. Les valeurs `short` et `full` ne doivent pas être identiques.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Nom complet court de l’application.|
|`full`|100 caractères||Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.|

## <a name="description"></a>description

**Obligatoire**

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.

Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience. Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation. Les valeurs `short` et `full` ne doivent pas être identiques.  Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4000 caractères|✔|Description complète de votre application.|

## <a name="icons"></a>icons

**Obligatoire**

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de téléchargement. Pour plus d’informations, consultez la rubrique [Icons](~/concepts/build-and-test/apps-package.md#icons) .

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|2 048 caractères|✔|Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.|
|`color`|2 048 caractères|✔|Chemin d’accès relatif à une icône PNG 192x192 couleur complète.|

## <a name="accentcolor"></a>accentColor

**Obligatoire** &ndash; Chaîne

Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # », par exemple `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans l’étendue teams et un seul onglet par application est pris en charge.

L’objet est un tableau contenant tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une solution de sous-onglet canal configurable.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|String|2 048 caractères|✔|URL https://à utiliser lors de la configuration de l’onglet.|
|`canUpdateConfiguration`|Booléen|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Default`true`|
|`scopes`|Tableau de l’énum|1 |✔|Actuellement, les onglets configurables prennent en charge uniquement les `team` `groupchat` étendues et. |
|`sharePointPreviewImage`|String|2048||Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint. Taille 1024 x 768. |
|`supportedSharePointHosts`|Tableau de l’énum|1 ||Définit la manière dont votre onglet sera disponible dans SharePoint. Les options sont `sharePointFullPage` et`sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans l' `team` étendue ne sont pas pris en charge actuellement.

L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|String|64 caractères|✔|Identificateur unique de l’entité que l’onglet affiche.|
|`name`|String|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|String|2 048 caractères|✔|URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.|
|`websiteUrl`|String|2 048 caractères||URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.|
|`scopes`|Tableau de l’énum|1 |✔|Actuellement, les onglets statiques prennent en charge uniquement l' `personal` étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.|

> [!NOTE]
> Si vos onglets nécessitent des informations contextuelles pour afficher le contenu pertinent ou pour initier un flux d’authentification, *reportez-vous* à [la rubrique obtenir le contexte de votre onglet Microsoft teams](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

**Optional**

Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’objet est un tableau (maximum d’un seul élément &mdash; , actuellement un seul bot est autorisé par application) à tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Il peut s’agir de la même chose que l' [ID d’application](#id)global.|
|`needsChannelSelector`|Booléen|||Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique. Default`false`|
|`isNotificationOnly`|Booléen|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. Default`false`|
|`supportsFiles`|Boolean|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. Default`false`|
|`scopes`|Tableau de l’énum|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|

### <a name="botscommandlists"></a>bots. commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot. Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau de l’énum|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10 |✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

## <a name="connectors"></a>ceux

**Optional**

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|String|2 048 caractères|✔|URL https://à utiliser lors de la configuration du connecteur.|
|`connectorId`|String|64 caractères|✔|Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).|
|`scopes`|Tableau de l’énum|1 |✔|Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel ( `personal` ). Actuellement, seule l' `team` étendue est prise en charge.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.

L’objet est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64|✔|ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot. Il peut s’agir de la même chose que l’ID d’application global.|
|`canUpdateConfiguration`|Booléen|||Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. La valeur par défaut est `false` .|
|`commands`|Tableau d’objets|10 |✔|Tableau de commandes prises en charge par l’extension de messagerie|
|`messageHandlers`|Tableau d’objets|5 ||Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies. Les domaines doivent également être affichés dans`validDomains`|
|`messageHandlers.type`|String|||Type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|Tableau de chaînes|||Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.|

### <a name="composeextensionscommands"></a>composeExtensions. Commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur. Il y a un maximum de 10 commandes.

Chaque élément de commande est un objet de la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|64 caractères|✔|ID de la commande|
|`type`|String|64 caractères||Type de la commande. L’une `query` ou l’autre `action` . Default`query`|
|`title`|String|32 caractères|✔|Nom de commande convivial|
|`description`|String|128 caractères||La description qui s’affiche pour les utilisateurs afin d’indiquer la finalité de cette commande.|
|`initialRun`|Booléen|||Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre. Default`false`|
|`context`|Tableau de chaînes|3||Définit l’emplacement à partir duquel l’extension de message peut être appelée. Toute combinaison de `compose` , `commandBox` , `message` . Valeur par défaut est`["compose", "commandBox"]`|
|`fetchTask`|Booléen|||Une valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.|
|`taskInfo`|Objet|||Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie|
|`taskInfo.title`|String|64||Titre de la boîte de dialogue initiale|
|`taskInfo.width`|String|||Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »|
|`taskInfo.height`|String|||Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyen » ou « petite »|
|`taskInfo.url`|String|||URL d’affichage WebView initiale|
|`parameters`|Tableau d’objets|5 |✔|La liste des paramètres que la commande prend. Minimum : 1 ; maximum : 5|
|`parameter.name`|String|64 caractères|✔|Nom du paramètre tel qu’il apparaît dans le client. Elle est incluse dans la demande de l’utilisateur.|
|`parameter.title`|String|32 caractères|✔|Titre convivial du paramètre.|
|`parameter.description`|String|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameter.inputType`|String|128 caractères||Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` . ,,,,,, `text` `textarea` `number` `date` `time` `toggle``choiceset`|
|`parameter.choices`|Tableau d’objets|10 ||Options de choix pour le `choiceset` . À utiliser uniquement lorsque `parameter.inputType` est`choiceset`|
|`parameter.choices.title`|String|128||Titre du choix|
|`parameter.choices.value`|String|512||Valeur du choix|

## <a name="permissions"></a>autorisations

**Optional**

Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension. Les options suivantes ne sont pas exclusives :

* `identity`&emsp;Nécessite des informations d’identité d’utilisateur
* `messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe

Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour. Pour plus d’informations, consultez [la rubrique mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** Tableau de chaînes

Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif** **, sauf indication contraire**

Une liste des domaines valides pour les sites Web que l’application prévoit de charger dans le client Teams. Les listes de domaine peuvent inclure des caractères génériques, par exemple `*.example.com` . Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com` . Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.

Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

Les applications teams qui requièrent leurs propres URL SharePoint pour fonctionner correctement, peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais n' `*.onmicrosoft.com` est pas valide.

L’objet est un tableau contenant tous les éléments du type `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|36 caractères|✔|ID de l’application AAD de l’application. Cet ID doit être un GUID.|
|`resource`|String|2 048 caractères|✔|URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.|
