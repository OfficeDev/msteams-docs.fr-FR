---
title: Référence du schéma de manifeste de l’aperçu développeur
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: Aperçu des développeurs de schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673561"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Schéma de manifeste de l’aperçu développeur pour Microsoft teams

> [!NOTE]
> Pour plus d’informations sur le programme et sur la procédure de participation, voir [developer preview](~/resources/dev-preview/developer-preview-intro.md) .
> Si vous n’utilisez pas l’aperçu du développeur, vous ne devez pas utiliser cette version du manifeste. Voir [référence : schéma de manifeste pour Microsoft teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.

Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams. Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).

Pour plus d’informations sur les fonctionnalités disponibles, voir : [Features in the public developer preview for Microsoft teams](~/resources/dev-preview/developer-preview-features.md).

## <a name="sample-full-manifest"></a>Exemple de manifeste complet

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
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
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
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
          "type" : "search",
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
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
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
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
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

*Facultatif, mais chaîne recommandée* &ndash;

URL https://référençant le schéma JSON du manifeste.

## <a name="manifestversion"></a>manifestVersion

Chaîne **obligatoire** &ndash;

Version du schéma de manifeste utilisé par ce manifeste. Il doit être « devPreview ».

## <a name="version"></a>version

Chaîne **obligatoire** &ndash;

Version de l’application spécifique. Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée. Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités. Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé. Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.

Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.

Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).

## <a name="id"></a>id

ID d’application Microsoft **requis** &ndash;

Identificateur unique généré par Microsoft pour cette application. Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici. Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous [Ajoutez un bot](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName

Chaîne **obligatoire** &ndash;

Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.

## <a name="developer"></a>developer

**Obligatoire**

Spécifie les informations relatives à votre société. Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔|URL https://vers le site Web du développeur. Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.|
|`privacyUrl`|2 048 caractères|✔|URL https://vers la stratégie de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|L’URL https://vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères|✔|**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires. Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`|4 caractères|✔|Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant des traductions de langue supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`|4 caractères|✔|Balise de langue des chaînes dans le fichier fourni.|
|`file`|4 caractères|✔|Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.|

## <a name="name"></a>nom

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

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de téléchargement.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|2 048 caractères|✔|Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.|
|`color`|2 048 caractères|✔|Chemin d’accès relatif à une icône PNG 192x192 couleur complète.|

## <a name="accentcolor"></a>accentColor

Chaîne **obligatoire** &ndash;

Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # », par `#4464ee`exemple.

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans l’étendue teams et un seul onglet par application est pris en charge.

L’objet est un tableau contenant tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution de sous-onglet canal configurable.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔|URL https://à utiliser lors de la configuration de l’onglet.|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Default`true`|
|`scopes`|Tableau d’énumération|1 |✔|Actuellement, les onglets configurables prennent `team` en `groupchat` charge uniquement les étendues et. |
|`sharePointPreviewImage`|Chaîne|2048||Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint. Taille 1024 x 768. |
|`supportedSharePointHosts`|Tableau d’énumération|1 ||Définit la manière dont votre onglet sera disponible dans SharePoint. Les options `sharePointFullPage` sont et`sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques `team` déclarés dans l’étendue ne sont pas pris en charge actuellement.

L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|Chaîne|64 caractères|✔|Identificateur unique de l’entité que l’onglet affiche.|
|`name`|Chaîne|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|Chaîne|2 048 caractères|✔|URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.|
|`websiteUrl`|Chaîne|2 048 caractères||URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.|
|`scopes`|Tableau d’énumération|1 |✔|Actuellement, les onglets statiques `personal` prennent en charge uniquement l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.|

## <a name="bots"></a>bots

**Optional**

Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’objet est un tableau (maximum d’un seul élément&mdash;, actuellement un seul bot est autorisé par application) à tous les éléments du `object`type. Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|Chaîne|64 caractères|✔|ID d’application Microsoft unique pour le bot enregistré avec l’infrastructure bot. Il peut s’agir de la même chose que l' [ID d’application](#id)global.|
|`needsChannelSelector`|Boolean|||Indique si le bot utilise un Conseil de l’utilisateur pour ajouter le bot à un canal spécifique. Default`false`|
|`isNotificationOnly`|Boolean|||Indique si un bot est un robot à sens unique, par opposition à un bot de conversation. Default`false`|
|`supportsFiles`|Boolean|||Indique si le bot prend en charge la possibilité de télécharger ou de télécharger des fichiers dans une conversation personnelle. Default`false`|
|`scopes`|Tableau d’énumération|3 |✔|Indique si le bot offre une expérience dans le contexte d’un canal dans un `team`, dans une conversation de groupe`groupchat`() ou dans une expérience étendue à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|

### <a name="botscommandlists"></a>bots. commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments `object`de type ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot. Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|Tableau d’énumération|3 |✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options `team`sont `personal`, et `groupchat`.|
|`items.commands`|Tableau d’objets|10 |✔|Tableau de commandes pris en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description`: description simple ou exemple de la syntaxe de commande et de son argument (String, 128)|

## <a name="connectors"></a>ceux

**Optional**

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type. Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔|URL https://à utiliser lors de la configuration du connecteur.|
|`connectorId`|Chaîne|64 caractères|✔|Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).|
|`scopes`|Tableau d’énumération|1 |✔|Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team`, ou une expérience étendue à un utilisateur individuel (`personal`). Actuellement, seule l' `team` étendue est prise en charge.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.

L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type. Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|Chaîne|64|✔|ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot. Il peut s’agir de la même chose que l' [ID d’application](#id)global.|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. La valeur par `false`défaut est.|
|`commands`|Tableau d’objets|10 |✔|Tableau de commandes prises en charge par l’extension de messagerie|

### <a name="composeextensionscommands"></a>composeExtensions. Commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur. Il y a un maximum de 10 commandes.

Chaque élément de commande est un objet de la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|Chaîne|64 caractères|✔|ID de la commande|
|`type`|Chaîne|64 caractères||Type de la commande. L’une `query` ou `action`l’autre. Default`query`|
|`title`|Chaîne|32 caractères|✔|Nom de commande convivial|
|`description`|Chaîne|128 caractères||La description qui s’affiche pour les utilisateurs afin d’indiquer la finalité de cette commande.|
|`initialRun`|Boolean|||Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre. Default`false`|
|`context`|Tableau de chaînes|3 ||Définit l’emplacement à partir duquel l’extension de message peut être appelée. Toute combinaison de `compose`, `commandBox`, `message`. Valeur par défaut est`["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Une valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.|
|`taskInfo`|Objet|||Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie|
|`taskInfo.title`|Chaîne|64||Titre de la boîte de dialogue initiale|
|`taskInfo.width`|Chaîne|||Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »|
|`taskInfo.height`|Chaîne|||Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyen » ou « petite »|
|`taskInfo.url`|Chaîne|||URL d’affichage WebView initiale|
|`messageHandlers`|Tableau d’objets|5 ||Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies. Les domaines doivent également être affichés dans`validDomains`|
|`messageHandlers.type`|Chaîne|||Type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|Tableau de chaînes|||Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.|
|`parameters`|Tableau d’objets|5 |✔|La liste des paramètres que la commande prend. Minimum : 1 ; maximum : 5|
|`parameter.name`|Chaîne|64 caractères|✔|Nom du paramètre tel qu’il apparaît dans le client. Elle est incluse dans la demande de l’utilisateur.|
|`parameter.title`|Chaîne|32 caractères|✔|Titre convivial du paramètre.|
|`parameter.description`|Chaîne|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameter.inputType`|Chaîne|128 caractères||Définit le type de contrôle affiché sur un module de tâche `fetchTask: true`pour. `text` `textarea` `number`, `date`,, `time` `toggle``choiceset`|
|`parameter.choices`|Tableau d’objets|10 ||Options de choix pour le `choiceset`. À utiliser uniquement `parameter.inputType` lorsque est`choiceset`|
|`parameter.choices.title`|Chaîne|128||Titre du choix|
|`parameter.choices.value`|Chaîne|512||Valeur du choix|

## <a name="permissions"></a>autorisations

**Optional**

Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension. Les options suivantes ne sont pas exclusives :

* `identity`&emsp; Nécessite des informations d’identité d’utilisateur
* `messageTeamMembers`&emsp; Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe

Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** Tableau de chaînes

Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès. Les options sont les suivantes :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif** **, sauf indication contraire**

Une liste des domaines valides à partir desquels l’application prévoit de charger tout contenu. Les listes de domaine peuvent inclure des caractères génériques `*.example.com`, par exemple. Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com`. Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.

Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne `validDomains[]`devez pas inclure Accounts.google.com dans.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau contenant tous les éléments du type `string`.

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|Chaîne|36 caractères|✔|ID de l’application AAD de l’application. Cet ID doit être un GUID.|
|`resource`|Chaîne|2 048 caractères|✔|URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.|