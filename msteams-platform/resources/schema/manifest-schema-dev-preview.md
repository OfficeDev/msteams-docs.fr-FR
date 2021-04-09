---
title: Référence du schéma de manifeste d’aperçu du développeur
description: Décrit le schéma pris en charge par le manifeste pour Microsoft Teams
ms.topic: reference
keywords: Aperçu du schéma de manifeste teams pour les développeurs
ms.date: 05/20/2019
ms.openlocfilehash: f8c1842d6b9f9d07d8743f5bf7f868cacbd282af
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634487"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Schéma de manifeste de prévisualisation pour les développeurs pour Microsoft Teams

> [!NOTE]
> Pour plus [d’informations](~/resources/dev-preview/developer-preview-intro.md) sur le programme et la façon dont vous pouvez participer, voir Aperçu du développeur.
> Si vous n’utilisez pas la prévisualisation du développeur, vous ne devez pas utiliser cette version du manifeste. Voir [la référence : schéma de manifeste pour Microsoft Teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.

Le manifeste De Microsoft Teams décrit comment l’application s’intègre au produit Microsoft Teams. Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .

Pour plus d’informations sur les fonctionnalités disponibles, voir : Fonctionnalités de la prévisualisation pour [les développeurs publics pour Microsoft Teams.](~/resources/dev-preview/developer-preview-features.md)

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
  ],
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

*Facultatif, mais recommandé* &ndash; Chaîne

L https:// URL référente au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifestVersion

**Obligatoire** &ndash; Chaîne

Version du schéma de manifeste utilisé par ce manifeste. Il doit s’appelle « devPreview ».

## <a name="version"></a>version

**Obligatoire** &ndash; Chaîne

Version de l’application spécifique. Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée. Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités. Si cette application a été soumise au Store, le nouveau manifeste devra être soumis à nouveau et validé à nouveau. Ensuite, les utilisateurs de cette application obtiennent automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.

Si l’application demande des autorisations, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.

Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatoire** &ndash; ID d’application Microsoft

Identificateur unique généré par Microsoft pour cette application. Si vous avez inscrit un bot via Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un ID et l’entrer ici. Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft[(Mes applications),](https://apps.dev.microsoft.com)entrez-le ici, puis réutilisez-le lorsque vous [ajoutez un bot.](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="packagename"></a>packageName

**Obligatoire** &ndash; Chaîne

Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com.example.myapp.

## <a name="developer"></a>developer

**Obligatoire**

Spécifie des informations sur votre entreprise. Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations de votre entrée AppSource.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔|L https:// URL du site web du développeur. Ce lien doit permettre aux utilisateurs d’accès à votre entreprise ou à votre page d’accueil spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔|L https:// URL vers la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|L https:// URL vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères|✔|**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

Autorise la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires. Voir [localisation.](~/concepts/build-and-test/apps-localization.md)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`|4 caractères|✔|Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant des traductions linguistiques supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`|4 caractères|✔|Balise de langue des chaînes dans le fichier fourni.|
|`file`|4 caractères|✔|Chemin d’accès relatif au fichier .json contenant les chaînes traduites.|

## <a name="name"></a>nom

**Obligatoire**

Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience Teams. Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs `short` de et ne doivent pas être `full` identiques.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Nom d’affichage court de l’application.|
|`full`|100 caractères||Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Obligatoire**

Décrit votre application aux utilisateurs. Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience. Notez également, dans la description complète, si un compte externe est requis pour être utilisé. Les valeurs `short` de et ne doivent pas être `full` identiques.  Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4 000 caractères|✔|Description complète de votre application.|

## <a name="icons"></a>icons

**Obligatoire**

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de chargement.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|2 048 caractères|✔|Chemin d’accès relatif à un plan PNG transparent 32 x 32.|
|`color`|2 048 caractères|✔|Chemin d’accès relatif à une icône PNG couleur 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Obligatoire** &ndash; Chaîne

Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans l’étendue Teams, et actuellement, un seul onglet par application est pris en charge.

L’objet est un tableau avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet de canal configurable.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔|Url https:// à utiliser lors de la configuration de l’onglet.|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Valeur par défaut : `true`|
|`scopes`|Tableau de l’énum|1|✔|Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues. |
|`sharePointPreviewImage`|Chaîne|2048||Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint. Taille 1024 x 768. |
|`supportedSharePointHosts`|Tableau de l’énum|1||Définit la façon dont votre onglet sera disponible dans SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.

L’objet est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|String|64 caractères|✔|Identificateur unique de l’entité affichée par l’onglet.|
|`name`|Chaîne|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|Chaîne|2 048 caractères|✔|Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans le canevas Teams.|
|`websiteUrl`|Chaîne|2 048 caractères||L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.|
|`scopes`|Tableau de l’énum|1|✔|Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.|

## <a name="bots"></a>bots

**Optional**

Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’objet est un tableau (jusqu’à un seul élément actuellement un seul bot est autorisé par application) avec tous les &mdash; éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela peut être identique à [l’ID d’application global.](#id)|
|`needsChannelSelector`|Boolean|||Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique. Valeur par défaut : `false`|
|`isNotificationOnly`|Boolean|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. Valeur par défaut : `false`|
|`supportsFiles`|Boolean|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. Valeur par défaut : `false`|
|`scopes`|Tableau de l’énum|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|

### <a name="botscommandlists"></a>bots.commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge. Pour plus [d’informations,](~/bots/how-to/create-a-bot-commands-menu.md) voir les menus du bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau de l’énum|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10 |✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

## <a name="connectors"></a>connecteurs

**Optional**

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔|Url https:// à utiliser lors de la configuration du connecteur.|
|`connectorId`|String|64 caractères|✔|Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)|
|`scopes`|Tableau de l’énum|1|✔|Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ). Actuellement, seule `team` l’étendue est prise en charge.|

## <a name="composeextensions"></a>composeExtensions

**Optional**

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.

L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Obligatoire | Description|
|---|---|---|---|---|
|`botId`|Chaîne|64|✔|ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework. Cela peut être identique à [l’ID d’application global.](#id)|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. La valeur par défaut `false` est .|
|`commands`|Tableau d’objets|10 |✔|Tableau de commandes pris en charge par l’extension de messagerie|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur. Il existe un maximum de 10 commandes.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|64 caractères|✔|ID de la commande|
|`type`|String|64 caractères||Type de la commande. L’un `query` ou `action` l’autre . Valeur par défaut : `query`|
|`title`|Chaîne|32 caractères|✔|Nom de la commande conviviale|
|`description`|Chaîne|128 caractères||Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande|
|`initialRun`|Boolean|||Valeur boolé américaine qui indique si la commande doit être exécuté initialement sans paramètre. Valeur par défaut : `false`|
|`context`|Tableau de chaînes|3||Définit l’endroit à partir de lequel l’extension de message peut être invoquée. N’importe quelle `compose` combinaison de `commandBox` , `message` . La valeur par défaut est `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||Valeur booléle qui indique si le module de tâche doit être récupéré dynamiquement|
|`taskInfo`|Objet|||Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie|
|`taskInfo.title`|Chaîne|64||Titre de la boîte de dialogue initiale|
|`taskInfo.width`|Chaîne|||Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite »|
|`taskInfo.height`|Chaîne|||Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite »|
|`taskInfo.url`|Chaîne|||URL webview initiale|
|`messageHandlers`|Tableau d’objets|5 ||Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies. Les domaines doivent également être répertoriés dans `validDomains`|
|`messageHandlers.type`|Chaîne|||Type de handler de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|Tableau de chaînes|||Tableau de domaines pour l’inscription du handler de message de lien.|
|`parameters`|Tableau d’objets|5 |✔|Liste des paramètres pris par la commande. Minimum : 1 ; maximum : 5|
|`parameter.name`|String|64 caractères|✔|Nom du paramètre tel qu’il apparaît dans le client. Ceci est inclus dans la demande de l’utilisateur.|
|`parameter.title`|Chaîne|32 caractères|✔|Titre convivial du paramètre.|
|`parameter.description`|Chaîne|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameter.inputType`|Chaîne|128 caractères||Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` . `text`L’un des , , , , `textarea` `number` `date` `time` `toggle` ,`choiceset`|
|`parameter.choices`|Tableau d’objets|10 ||Options de choix pour `choiceset` le . Utiliser uniquement lorsque `parameter.inputType` c’est le cas `choiceset`|
|`parameter.choices.title`|Chaîne|128||Titre du choix|
|`parameter.choices.value`|Chaîne|512||Valeur du choix|

## <a name="permissions"></a>autorisations

**Optional**

Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` l’extension va s’exécuter. Les options suivantes ne sont pas exclusives :

* `identity`&emsp;Nécessite des informations d’identité d’utilisateur
* `messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe

La modification de ces autorisations lors de la mise à jour de votre application entraîne la répétition du processus de consentement par vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** Tableau de chaînes

Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application peut demander l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué

Liste des domaines valides à partir des lesquels l’application s’attend à charger du contenu. Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple. Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` . Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.

**Toutefois, il** n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Spécifiez votre ID d’application AAD et les informations Graph pour aider les utilisateurs à se connecter en toute transparence à votre application AAD.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|Chaîne|36 caractères|✔|ID d’application AAD de l’application. Cet ID doit être un GUID.|
|`resource`|Chaîne|2 048 caractères|✔|URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.|

## <a name="configurableproperties"></a>configurableProperties

**Facultatif** - tableau

Le `configurableProperties` bloc définit les propriétés d’application que l’administrateur Teams peut personnaliser. Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams.](/MicrosoftTeams/customize-apps)

> [!NOTE]
> Au moins une propriété doit être définie. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.
> En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application. 

Vous pouvez définir l’une des propriétés suivantes :
* `name`: permet à l’administrateur de modifier le nom complet de l’application.
* `shortDescription`: permet à l’administrateur de modifier la description courte de l’application.
* `longDescription`: permet à l’administrateur de modifier la description détaillée de l’application.
* `smallImageUrl`: il `outline` s’agit de la propriété dans le bloc du `icons` manifeste.
* `largeImageUrl`: il s’agit `color` de la propriété dans le bloc du `icons` manifeste.
* `accentColor`: il s’agit de la couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.
* `developerUrl`: il s’agit https:// URL du site web du développeur.
* `privacyUrl`: il s’agit https:// URL de la politique de confidentialité du développeur.
* `termsOfUseUrl`: il s’agit https:// URL des conditions d’utilisation du développeur.


