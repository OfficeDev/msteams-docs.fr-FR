---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: medium
keywords: schéma de manifeste teams
ms.openlocfilehash: 07b2c969877dc61c8678bb89099d6275f2cf367c
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475758"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Référence : schéma de manifeste pour Microsoft Teams

Le Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit. Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) . Les versions précédentes 1.0, 1.1,..., et 1.6 sont également pris en charge (à l’aide de « v1.x » dans l’URL).
Pour plus d’informations sur les modifications apportées dans chaque version, voir [le journal des modifications du manifeste.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)

L’exemple de schéma suivant montre toutes les options d’extensibilité :

## <a name="sample-full-manifest"></a>Exemple de manifeste complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
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
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
  ],
  "validDomains": [
    "contoso.com",
    "mysite.someplace.com",
    "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ]
  },
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
  "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

Chaîne facultative, mais recommandée

L https:// URL référente au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifestVersion

**Obligatoire**— chaîne

Version du schéma de manifeste que ce manifeste utilise. Elle doit être 1,10.

## <a name="version"></a>version

**Obligatoire**— chaîne

Version d’une application spécifique. Lorsque vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée. De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité. Lorsque cette application a été soumise au Store, le nouveau manifeste doit être soumis à nouveau et revalidé. Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.

Si l’application demande des autorisations change, les utilisateurs sont invités à mettre à niveau et à se reconsenter à l’application.

Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatoire**: ID d’application Microsoft

L’ID est un identificateur unique généré par Microsoft pour l’application. Vous avez un ID si votre bot est inscrit via le Microsoft Bot Framework. Vous avez un ID si l’application web de votre onglet se signe déjà avec Microsoft. Vous devez entrer l’ID ici. Sinon, vous devez générer un nouvel ID sur le portail [d’inscription des applications Microsoft.](https://aka.ms/appregistrations) Utilisez le même ID si vous ajoutez un bot.

> [!NOTE]
> Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.

## <a name="developer"></a>developer

**Obligatoire**— objet

Spécifie des informations sur votre entreprise. Pour les applications envoyées au Teams store, ces valeurs doivent correspondre aux informations de votre listing dans le Windows Store. Pour plus d’informations, voir les Teams [de publication du Store.](~/concepts/deploy-and-publish/appsource/publish.md)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔|L https:// URL du site web du développeur. Ce lien doit prendre les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔|L https:// URL vers la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|L https:// URL vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères| |**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="name"></a>nom

**Obligatoire**— objet

Nom de l’expérience de votre application, affiché aux utilisateurs dans l’Teams expérience utilisateur. Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs `short` de et doivent être `full` différentes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Nom d’affichage court de l’application.|
|`full`|100 caractères||Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Obligatoire**— objet

Décrit votre application aux utilisateurs. Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrit votre expérience et aide les clients potentiels à comprendre ce que fait votre expérience. Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé. Les valeurs `short` de et doivent être `full` différentes. Votre description courte ne peut pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4 000 caractères|✔|Description complète de votre application.|

## <a name="packagename"></a>packageName

**Facultatif**— chaîne

Identificateur unique de l’application dans la notation de domaine inverse ; par exemple, com.example.myapp. Longueur maximale : 64 caractères.

## <a name="localizationinfo"></a>localizationInfo

**Facultatif**— objet

Autorise la spécification d’une langue par défaut et fournit des pointeurs vers d’autres fichiers de langue. Pour plus d’informations, [voir localisation.](~/concepts/build-and-test/apps-localization.md)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant davantage de traductions linguistiques.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`||✔|Balise de langue des chaînes dans le fichier fourni.|
|`file`||✔|Chemin d’accès relatif au fichier .json contenant les chaînes traduites.|

## <a name="icons"></a>icons

**Obligatoire**— objet

Icônes utilisées dans l’Teams app. Les fichiers d’icône doivent être inclus dans le package de chargement. Pour plus d’informations, voir [Icônes.](../../concepts/build-and-test/apps-package.md#app-icons)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|32 x 32 pixels|✔|Chemin d’accès relatif à un plan PNG transparent 32 x 32.|
|`color`|192 x 192 pixels|✔|Chemin d’accès relatif à une icône PNG couleur 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Facultatif**— Code de couleur HTML Hex

Couleur à utiliser et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.

## <a name="configurabletabs"></a>configurableTabs

**Facultatif**— tableau

Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans les étendues et les étendues et vous pouvez configurer les mêmes `team` `groupchat` onglets plusieurs fois. Toutefois, vous ne pouvez la définir dans le manifeste qu’une seule fois.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|Url https:// à utiliser lors de la configuration de l’onglet.|
|`scopes`|tableau d’enums|1|✔|Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues. |
|`canUpdateConfiguration`|booléen|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Valeur par défaut **: true**.|
|`context` |tableau d’enums|6 ||Ensemble `contextItem` d’étendues où un [onglet est pris en charge.](../../tabs/how-to/access-teams-context.md) Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint. Taille 1024 x 768. |
|`supportedSharePointHosts`|tableau d’enums|1||Définit la façon dont votre onglet est mis à disposition dans SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Facultatif**— tableau

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.

Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|string|64 caractères|✔|Identificateur unique de l’entité affichée par l’onglet.|
|`name`|string|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|string||✔|Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone Teams dessin.|
|`websiteUrl`|string|||L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.|
|`searchUrl`|string|||L https:// URL pointant vers les requêtes de recherche d’un utilisateur.|
|`scopes`|tableau d’enums|1|✔|Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.|
|`context` | tableau d’enums| 2|| Ensemble `contextItem` d’étendues où un onglet est pris en charge.|

> [!NOTE]
>  La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.
> Si vos onglets nécessitent des informations contextielles pour afficher du contenu pertinent ou pour lancer un flux d’authentification, pour plus d’informations, voir Obtenir le contexte de [votre onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>bots

**Facultatif**— tableau

Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’élément est un tableau (un seul élément est actuellement autorisé par application) avec tous les éléments &mdash; du type `object` . Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. L’ID peut être identique à [l’ID d’application global.](#id)|
|`scopes`|tableau d’enums|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|
|`needsChannelSelector`|valeur booléenne|||Indique si le bot utilise ou non un conseil de l’utilisateur pour ajouter le bot à un canal spécifique. Valeur par défaut : **`false`**|
|`isNotificationOnly`|valeur booléenne|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. Valeur par défaut : **`false`**|
|`supportsFiles`|valeur booléenne|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. Valeur par défaut : **`false`**|
|`supportsCalling`|valeur booléenne|||Valeur indiquant où un bot prend en charge les appels audio. **IMPORTANT**: cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Valeur par défaut : **`false`**|
|`supportsVideo`|valeur booléenne|||Valeur indiquant où un bot prend en charge les appels vidéo. **IMPORTANT**: cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Valeur par défaut : **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de deux éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge. Pour plus d’informations, voir [menus bot.](~/bots/how-to/create-a-bot-commands-menu.md)

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau d’enums|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10|✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|title|string|12 |✔|Nom de la commande du bot.|
|description|string|128 caractères|✔|Description de texte simple ou exemple de syntaxe de commande et de ses arguments.|

## <a name="connectors"></a>connecteurs

**Facultatif**— tableau

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum d’un élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|Url https:// à utiliser lors de la configuration du connecteur.|
|`scopes`|tableau d’enums|1|✔|Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ). Actuellement, seule `team` l’étendue est prise en charge.|
|`connectorId`|string|64 caractères|✔|Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Facultatif**— tableau

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.

L’élément est un tableau (maximum d’un élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Obligatoire | Description|
|---|---|---|---|---|
|`botId`|string|64|✔|ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework. L’ID peut être identique à l’ID d’application global.|
|`commands`|tableau d’objets|10|✔|Tableau de commandes pris en charge par l’extension de messagerie.|
|`canUpdateConfiguration`|booléen|||Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. Par défaut : **false**.|
|`messageHandlers`|tableau d’objets|5||Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.|
|`messageHandlers.type`|string|||Type de handler de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|tableau de chaînes|||Tableau de domaines pour l’inscription du handler de message de lien.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes avec un maximum de 10 commandes. Chaque commande s’affiche Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|64 caractères|✔|ID de la commande.|
|`title`|string|32 caractères|✔|Nom de la commande conviviale.|
|`type`|string|64 caractères||Type de la commande. L’un `query` ou `action` l’autre . Par défaut : **requête**.|
|`description`|string|128 caractères||Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.|
|`initialRun`|booléen|||Une valeur booléle indique si la commande s’exécute initialement sans paramètre. La valeur par défaut est **False**.|
|`context`|tableau de chaînes|3||Définit l’endroit à partir de lequel l’extension de message peut être invoquée. N’importe quelle `compose` combinaison de `commandBox` , `message` . La valeur par défaut est `["compose","commandBox"]`.|
|`fetchTask`|booléen|||Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche. La valeur par défaut est **False**.|
|`taskInfo`|objet|||Spécifiez le module de tâche à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.|
|`taskInfo.title`|string|64 caractères||Titre de la boîte de dialogue initiale.|
|`taskInfo.width`|string|||Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».|
|`taskInfo.height`|string|||Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».|
|`taskInfo.url`|string|||URL webview initiale.|
|`parameters`|tableau d’objets|5 éléments|✔|Liste des paramètres pris par la commande. Minimum : 1 ; maximum : 5.|
|`parameters.name`|string|64 caractères|✔|Nom du paramètre tel qu’il apparaît dans le client. Le nom du paramètre est inclus dans la demande de l’utilisateur.|
|`parameters.title`|string|32 caractères|✔|Titre convivial du paramètre.|
|`parameters.description`|string|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameters.value`|string|512 caractères||Valeur initiale du paramètre.|
|`parameters.inputType`|string|128 caractères||Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` . L’une `text, textarea, number, date, time, toggle, choiceset` des .|
|`parameters.choices`|tableau d’objets|10 éléments||Options de choix pour `choiceset` le . Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.|
|`parameters.choices.title`|string|128 caractères|✔|Titre du choix.|
|`parameters.choices.value`|string|512 caractères|✔|Valeur du choix.|

## <a name="permissions"></a>autorisations

**Facultatif —** tableau de chaînes

Tableau de , qui spécifie les autorisations que l’application demande, qui indiquent aux utilisateurs finals le `string` fonctionnement de l’extension. Les options suivantes ne sont pas exclusives :

* `identity`&emsp;Nécessite des informations d’identité d’utilisateur.
* `messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.

Si vous modifiez ces autorisations pendant la mise à jour de l’application, vos utilisateurs répètent le processus de consentement après avoir exécuté l’application mise à jour. Pour plus d’informations, voir [Mise à jour de votre application.](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="devicepermissions"></a>devicePermissions

**Facultatif —** tableau de chaînes

Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué.

Liste des domaines valides pour les sites web que l’application s’attend à charger dans Teams client. Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` . Le domaine valide correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` . Si la configuration de votre onglet ou l’interface utilisateur de contenu navigue vers un autre domaine que la configuration de l’onglet, ce domaine doit être spécifié ici.

**N’incluez** pas les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

Teams applications qui nécessitent leurs propres URL de SharePoint pour fonctionner, inclut « {teamsitedomain} » dans leur liste de domaines valide.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Facultatif**— objet

Fournissez votre ID d’Azure Active Directory (AAD) et des informations microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application. Si votre application est inscrite dans AAD, vous devez fournir l’ID de l’application. Les administrateurs peuvent facilement passer en revue les autorisations et accorder leur consentement dans Teams centre d’administration.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|36 caractères|✔|ID d’application AAD de l’application. Cet ID doit être un GUID.|
|`resource`|string|2 048 caractères|✔|URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso. </br> **REMARQUE :** Si vous n’utilisez pas l’oD SSO, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, pour éviter une réponse https://notapplicable d’erreur. |
|`applicationPermissions`|tableau de chaînes|128 caractères||Spécifiez le consentement précis [spécifique à une ressource.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Facultatif**— booléen

Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement. La valeur par défaut est **False**.
>[!NOTE]
>Si vous sélectionnez true dans le manifeste de votre application, pour charger la page correctement, modifiez les pages de contenu de vos onglets et modules de tâche comme décrit dans Afficher un document d’indicateur de chargement `showLoadingIndicator` natif. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)


## <a name="isfullscreen"></a>isFullScreen

 **Facultatif**— booléen

Indiquez l’endroit où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet. La valeur par défaut est **False**.

> [!NOTE]
> `isFullScreen`fonctionne uniquement avec SharePoint onglets et les applications du Store.

## <a name="activities"></a>activities

**Facultatif**— objet

Définissez les propriétés que votre application utilise pour publier un flux d’activités utilisateur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`activityTypes`|tableau d’objets|128 éléments| | Fournissez les types d’activités que votre application peut publier dans un flux d’activités des utilisateurs.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`type`|string|32 caractères|✔|Type de notification. *Voir ci-dessous.*|
|`description`|string|128 caractères|✔|Brève description de la notification. *Voir ci-dessous.*|
|`templateText`|string|128 caractères|✔|Ex: « {actor} created task {taskId} for you »|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a>defaultInstallScope

**Facultatif** - chaîne

Spécifie l’étendue d’installation définie par défaut pour cette application. L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application. Les options sont :
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Facultatif** - objet

Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application. Les options sont :
* `team`
* `groupchat`
* `meetings`
 
|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`team`|string|||Lorsque l’étendue d’installation sélectionnée `team` est , ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab` , `bot` ou `connector` .|
|`groupchat`|string|||Lorsque l’étendue d’installation sélectionnée `groupchat` est , ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab` , `bot` ou `connector` .|
|`meetings`|string|||Lorsque l’étendue d’installation sélectionnée `meetings` est , ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab` , `bot` ou `connector` .|

## <a name="configurableproperties"></a>configurableProperties

**Facultatif** - tableau

Le `configurableProperties` bloc définit les propriétés d’application que les administrateurs Teams personnaliser. Pour plus d’informations, voir [activer la personnalisation de l’application.](~/concepts/design/enable-app-customization.md)

> [!NOTE]
> Au moins une propriété doit être définie. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.

Vous pouvez définir l’une des propriétés suivantes :

* `name`: nom d’affichage de l’application.
* `shortDescription`: Description courte de l’application.
* `longDescription`: Description détaillée de l’application.
* `smallImageUrl`: Icône de plan de l’application.
* `largeImageUrl`: Icône de couleur de l’application.
* `accentColor`: couleur à utiliser et arrière-plan pour vos icônes de plan.
* `developerUrl`: URL HTTPS du site web du développeur.
* `privacyUrl`: URL HTTPS de la politique de confidentialité du développeur.
* `termsOfUseUrl`: URL HTTPS des conditions d’utilisation du développeur.
