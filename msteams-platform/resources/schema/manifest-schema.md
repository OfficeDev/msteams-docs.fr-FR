---
title: Référence du schéma du manifeste
description: Décrit le schéma du manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: high
keywords: schéma du manifeste teams
ms.openlocfilehash: 88fd025229a90ac6e3888763f643829950912633
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212018"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Référence : schéma du manifeste pour Microsoft Teams

Le manifeste Teams décrit comment l’application s’intègre au produit Microsoft Teams. Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json) . Les versions précédentes 1.0, 1.1,..., et 1.11 sont également pris en charge (à l’aide de « v1.x » dans l’URL).
Pour plus d’informations sur les modifications apportées dans chaque version, voir [le journal des modifications du manifeste.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)

L’exemple de schéma suivant montre toutes les options d’extensibilité :

## <a name="sample-full-manifest"></a>Exemple du manifeste complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
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
          "description": "Command Description; e.g., Add a customer",
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
        },
         {
          "id": "exampleCmd3",
          "title": "Example Command 3",
          "type": "action",
          "context": [
            "compose",
            "commandBox",
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "fetchTask": false,
          "taskInfo": {
            "title": "Initial dialog title",
            "width": "Dialog width",
            "height": "Dialog height",
            "url": "Initial webview URL"
          }
        }
      ],
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
  "defaultBlockUntilAdminAction": true,
  "publisherDocsUrl": "https://website.com/app-info",
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
 ],
  "subscriptionOffer": {
    "offerId": "publisherId.offerId"
  }
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

Chaîne facultative, mais recommandée

L’URL https:// fait référence au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifestVersion

**Obligatoire**— chaîne

Version du schéma du manifeste que ce manifeste utilise. Ce doit être 1,10.

## <a name="version"></a>version

**Obligatoire**— chaîne

Version d’une application spécifique. Lorsque vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée. De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité. Lorsque cette application a été soumise à Store, le nouveau manifeste doit être soumis à nouveau et revalidé. Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.

Si l’application demande le changement des autorisations, les utilisateurs sont invités à mettre à niveau et à se réinscrire à l’application.

Cette chaîne de version doit suivre la norme de [semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatoire** — ID d’application Microsoft

L’ID est un identificateur unique généré par Microsoft pour l’application. Vous avez un ID si votre bot est inscrit via le Microsoft Bot Framework. Vous avez un ID si l’application web de votre onglet se signe déjà avec Microsoft. Vous devez entrer l’ID ici. Sinon, vous devez générer un nouvel ID sur le [portail d’inscription des applications Microsoft.](https://aka.ms/appregistrations) Utilisez le même ID si vous ajoutez un bot.

> [!NOTE]
> Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.

## <a name="developer"></a>developer

**Obligatoire**— objet

Spécifie des informations sur votre entreprise. Pour les applications soumises au magasin Teams, ces valeurs doivent correspondre aux informations figurant dans votre description du magasin. Pour plus d’informations, voir les [instructions pour la publication dans les magasins Teams](~/concepts/deploy-and-publish/appsource/publish.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔|L’URL https:// du site web du développeur. Ce lien doit conduire les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔|L’URL https:// vers la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|L’URL https:// vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères| |**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="name"></a>nom

**Obligatoire**— objet

Nom de l’expérience de votre application, affiché à destination des utilisateurs dans l’expérience Teams. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs de `short` et `full` doivent être différentes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Nom d’affichage court de l’application.|
|`full`|100 caractères||Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Obligatoire**— objet

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrive votre expérience et aide les clients potentiels à comprendre ce que fait votre expérience. Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé. Les valeurs de `short` et `full` doivent être différentes. Votre description courte ne peut pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4 000 caractères|✔|Description complète de votre application.|

## <a name="packagename"></a>packageName

**Facultatif**— chaîne

Identificateur unique de l’application dans la notation de domaine inverse ; par exemple, com.example.myapp. Longueur maximale : 64 caractères.

## <a name="localizationinfo"></a>localizationInfo

**Facultatif**— objet

Autorise la spécification d’une langue par défaut et fournit des pointeurs vers d’autres fichiers de langue. Pour plus d’informations, voir [localisation.](~/concepts/build-and-test/apps-localization.md)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|La balise de langue des chaînes dans ce fichier du manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant davantage de traductions linguistiques.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`||✔|Balise de langue des chaînes dans le fichier fourni.|
|`file`||✔|Chemin d’accès relatif au fichier .json contenant les chaînes traduites.|

## <a name="icons"></a>icons

**Obligatoire**— objet

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de chargement. Pour plus d’informations, voir [Icônes](../../concepts/build-and-test/apps-package.md#app-icons).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|32 x 32 pixels|✔|Chemin d’accès relatif à un plan PNG transparent 32 x 32.|
|`color`|192 x 192 pixels|✔|Chemin d’accès relatif à une icône PNG couleur 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Obligatoire**— Code de couleur HTML Hex

Couleur à utiliser et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # » par exemple `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

**Facultatif**— tableau

Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans les étendues `team` et `groupchat` vous pouvez configurer les mêmes onglets plusieurs fois. Toutefois, vous ne pouvez la définir dans le manifeste qu’une seule fois.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|L’URL https:// à utiliser lors de la configuration de l’onglet.|
|`scopes`|tableau d’énumération|1|✔|Actuellement, les onglets configurables ne prennent en charge que les étendues `team` et `groupchat`. |
|`canUpdateConfiguration`|booléen|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Valeur par défaut : **true**.|
|`context` |tableau d’énumération|6 ||L’ensemble des `contextItem` étendues où un [onglet est pris en charge](../../tabs/how-to/access-teams-context.md). Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint. Taille 1024 x 768. |
|`supportedSharePointHosts`|tableau d’énumération|1||Définit la façon dont votre onglet est mis à disposition dans SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Facultatif**— tableau

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.

Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|string|64 caractères|✔|Identificateur unique de l’entité affichée par l’onglet.|
|`name`|chaîne|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|string||✔|L’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de canevas de Teams.|
|`websiteUrl`|string|||L’URL https:// pointant vers si un utilisateur choisit de l’afficher dans un navigateur.|
|`searchUrl`|chaîne|||L’URL https:// pointant vers les requêtes de recherche d’un utilisateur.|
|`scopes`|tableau d’énumération|1|✔|Actuellement, les onglets statiques ne peuvent prendre en charge que `personal` l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.|
|`context` | tableau d’énumération| 2|| L’ensemble `contextItem` des étendues où un onglet est pris en charge.|

> [!NOTE]
>  La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.
> Si vos onglets nécessitent des informations contextuelles pour afficher du contenu pertinent ou pour lancer un flux d’authentification, pour plus d’informations, voir [Obtenir le contexte de votre onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)

## <a name="bots"></a>bots

**Facultatif**— tableau

Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’élément est un tableau (maximum d’un seul élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. L’ID peut être identique à [l’ID d’application](#id) globale.|
|`scopes`|tableau d’énumération|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|
|`needsChannelSelector`|booléen|||Indique si le bot utilise ou non un conseil de l’utilisateur pour ajouter le bot à un canal spécifique. Par défaut :**`false`**|
|`isNotificationOnly`|booléen|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. Par défaut :**`false`**|
|`supportsFiles`|booléen|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. Par défaut :**`false`**|
|`supportsCalling`|booléen|||Valeur indiquant où un bot prend en charge les appels audio. **IMPORTANT** : Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Par défaut :**`false`**|
|`supportsVideo`|booléen|||Valeur indiquant où un bot prend en charge les appels vidéo. **IMPORTANT** : Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Par défaut :**`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de deux éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commandes distincte pour chaque étendue que votre bot prend en charge. Pour plus d’informations, voir [Menus bot.](~/bots/how-to/create-a-bot-commands-menu.md)

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau d’énumération|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10|✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|title|string|12 |✔|Nom de la commande du bot.|
|description|string|128 caractères|✔|Une description de texte simple ou exemple de syntaxe de commande et de ses arguments.|

## <a name="connectors"></a>connecteurs

**Facultatif**— tableau

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum d’un élément) avec tous les éléments de type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|L’URL https:// à utiliser lors de la configuration du connecteur.|
|`scopes`|tableau d’énumération|1|✔|Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un `team`, ou une expérience limitée à un utilisateur individuel seul (`personal`). Actuellement, seule l’étendue `team` est prise en charge.|
|`connectorId`|string|64 caractères|✔|Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Facultatif**— tableau

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom du manifeste reste le même pour que les extensions existantes continuent de fonctionner.

L’élément est un tableau (maximum d’un élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64|✔|L'ID de l'application Microsoft pour le bot qui accompagne l'extension de messagerie, tel qu’inscrit auprès de Bot Framework. L’ID peut être identique à l’ID d’application global.|
|`commands`|tableau d’objets|10|✔|Tableau de commandes pris en charge par l’extension de messagerie.|
|`canUpdateConfiguration`|booléen|||Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. Par défaut : **false**.|
|`messageHandlers`|tableau d’Objets|5||Liste des gestionnaires qui permettent d’appeler des applications lorsque certaines conditions sont remplies.|
|`messageHandlers.type`|string|||Type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|tableau de Chaînes|||Tableau de domaines pour lequel le gestionnaire de messages de lien peut s’inscrire.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes avec un maximum de 10 commandes. Chaque commande apparaît dans Microsoft Teams en tant qu’interaction potentielle à partir du point d’entrée basé sur l’IU.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|64 caractères|✔|ID de la commande.|
|`title`|chaîne|32 caractères|✔|Le nom de la commande conviviale.|
|`type`|string|64 caractères||Type de la commande. L’un des `query` ou `action`. Par défaut : **requête**.|
|`description`|chaîne|128 caractères||Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.|
|`initialRun`|booléen|||Une valeur booléenne indique si la commande s’exécute initialement sans les paramètres. La valeur par défaut est **False**.|
|`context`|tableau de Chaînes|3||Définit l’emplacement à partir duquel l’extension de message peut être appelée. N’importe quelle combinaison de `compose`,`commandBox` ,`message` . La valeur par défaut est `["compose","commandBox"]`.|
|`fetchTask`|booléen|||Une valeur booléenne qui indique s’il doit extraire dynamiquement le module de tâche. La valeur par défaut est **False**.|
|`taskInfo`|objet|||Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.|
|`taskInfo.title`|string|64 caractères||Titre de la boîte de dialogue initiale.|
|`taskInfo.width`|chaîne|||Largeur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.height`|string|||Hauteur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.url`|chaîne|||URL webview initiale.|
|`parameters`|tableau d'objet|5 éléments|✔|Liste des paramètres que prend la commande. Minimum : 1 ; maximum : 5.|
|`parameters.name`|string|64 caractères|✔|Nom du paramètre tel qu’il apparaît dans le client. Le nom du paramètre est inclus dans la demande de l’utilisateur.|
|`parameters.title`|chaîne|32 caractères|✔|Titre convivial du paramètre.|
|`parameters.description`|string|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameters.value`|string|512 caractères||Valeur initiale du paramètre. Actuellement, la valeur n’est pas prise en charge|
|`parameters.inputType`|string|128 caractères||Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` . L’un des `text, textarea, number, date, time, toggle, choiceset`.|
|`parameters.choices`|tableau d’objets|10 éléments||Options de choix pour le `choiceset`. Utilisez uniquement lorsque `parameter.inputType` est `choiceset`.|
|`parameters.choices.title`|string|128 caractères|✔|Titre du choix.|
|`parameters.choices.value`|string|512 caractères|✔|Valeur du choix.|

## <a name="permissions"></a>autorisations

**Facultatif** — tableau de chaînes

Tableau de `string`, qui spécifie les autorisations que l’application demande, qui indiquent aux utilisateurs finaux le fonctionnement de l’extension. Les options suivantes ne sont pas exclusives :

* `identity` &emsp;Nécessite des informations d’identité d’utilisateur.
* `messageTeamMembers` &emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.

La modification de ces autorisations pendant la mise à jour de l’application entraîne la répétition du processus de consentement par vos utilisateurs après l’exécution de l’application mise à jour. Pour plus d’informations, voir [Mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** — tableau de chaînes

Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif**, sauf **obligatoire** lorsque indiqué.

Liste des domaines valides pour les sites web que l’application s’attend à charger dans le client Teams. Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com`. Le domaine valide correspond exactement à un segment du domaine ; si vous devez faire correspondre `a.b.example.com` utilisez `*.*.example.com`. Si votre interface utilisateur de contenu ou de configuration d’onglet accède à un autre domaine que la configuration de tabulation, ce domaine doit être spécifié ici.

N’incluez **pas** les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com. Toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]`.

Les applications Teams qui nécessitent leurs propres URL SharePoint pour fonctionner correctement incluent « {teamsitedomain} » dans leur liste de domaines valide.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string`.

## <a name="webapplicationinfo"></a>WebApplicationInfo

**Facultatif**— objet

Fournissez votre ID d’application Azure Active Directory et vos informations de Microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application. Si votre application est inscrite dans Azure AD, vous devez fournir l’ID d’application. Les administrateurs peuvent facilement examiner les autorisations et accorder leur consentement dans le Centre d’administration Teams.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|36 caractères|✔|Application Azure AD ID d’application. Cet ID doit être un GUID.|
|`resource`|string|2 048 caractères|✔|URL de ressource de l’application pour l’acquisition du jeton du SSO. </br> **REMARQUE :** Si vous n’utilisez pas l’authentification unique, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, https://notapplicable pour éviter une réponse d’erreur. |
|`applicationPermissions`|tableau de chaînes|128 caractères||Spécifiez un consentement granulaire [spécifique à la ressource](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Facultatif**— booléen

Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement. La valeur par défaut est **False**.
>[!NOTE]
>Si vous sélectionnez`showLoadingIndicator` comme true dans le manifeste de votre application, pour charger correctement la page, modifiez les pages de contenu de vos onglets et modules de tâches, comme décrit dans le document [Afficher un indicateur de chargement natif](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).


## <a name="isfullscreen"></a>IsFullScreen

 **Facultatif**— booléen

Indiquez où une application personnelle est affichée avec ou sans barre d’en-tête d’onglet. La valeur par défaut est **False**.

> [!NOTE]
> `isFullScreen` fonctionne uniquement pour les applications publiées dans votre organisation.

## <a name="activities"></a>activités

**Facultatif**— objet

Définissez les propriétés utilisées par votre application pour publier un flux d’activité utilisateur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`activityTypes`|tableau d’Objets|128 éléments| | Indiquez les types d’activités que votre application peut publier dans un flux d’activités utilisateurs.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`type`|string|32 caractères|✔|Le type de notification. *Voir ci-dessous*.|
|`description`|string|128 caractères|✔|Une brève description de la notification. *Voir ci-dessous*.|
|`templateText`|string|128 caractères|✔|Exemple : « {actor} a créé la tâche {taskId} pour vous »|

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

**Facultatif**— chaîne

Spécifie l’étendue d’installation définie par défaut pour cette application. L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application. Les options sont :
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Facultatif**— objet

Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application. Les options sont :
* `team`
* `groupchat`
* `meetings`
 
|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`team`|string|||Lorsque l’étendue d’installation sélectionnée est `team`, ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab`, `bot`, ou `connector`.|
|`groupchat`|string|||Lorsque l’étendue d’installation sélectionnée est `groupchat`, ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab`, `bot`, ou `connector`.|
|`meetings`|string|||Lorsque l’étendue d’installation sélectionnée est `meetings`, ce champ spécifie la fonctionnalité par défaut disponible. Options : `tab`, `bot`, ou `connector`.|

## <a name="configurableproperties"></a>configurableProperties

**Facultatif**— tableau

Le bloc `configurableProperties` définit les propriétés d’application que les administrateurs Teams peuvent personnaliser. Pour plus d’informations, consultez [activer la personnalisation d’application](~/concepts/design/enable-app-customization.md). La fonctionnalité de personnalisation d’application n’est pas prise en charge dans les applications personnalisées ou LOB.

> [!NOTE]
> Au moins une propriété doit être définie. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.

Vous pouvez définir l’une des propriétés suivantes :

* `name` : Nom d’affichage de l’application.
* `shortDescription` : Description courte de l’application.
* `longDescription` : Description longue de l’application.
* `smallImageUrl` : Icône de contour de l’application.
* `largeImageUrl` : Icône de couleur de l’application.
* `accentColor` : Couleur à utiliser et arrière-plan pour vos icônes de contour.
* `developerUrl` : URL HTTPS du site web du développeur.
* `privacyUrl` : URL HTTPS de la politique de confidentialité du développeur.
* `termsOfUseUrl` : URL HTTPS des conditions d’utilisation du développeur.

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Facultatif**— booléen
 
Lorsque la propriété `defaultBlockUntilAdminAction` est définie sur **true**, l’application est masquée par défaut aux utilisateurs jusqu’à ce que l’administrateur l’autorise. Si la valeur est **true**, l’application est masquée pour tous les locataires et tous les utilisateurs finaux. Les administrateurs de locataire peuvent voir l’application dans le Centre d’administration Teams et prendre des mesures pour autoriser ou bloquer l’application. La valeur par défaut est **false**. Pour plus d’informations sur le bloc d’application par défaut, consultez [Masquer l’application Teams jusqu’à ce que l’administrateur approuve](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves).

## <a name="publisherdocsurl"></a>publisherDocsUrl

**Facultatif**— chaîne

**Maille maximale** — 128 caractères

Le `publisherDocsUrl` est une URL HTTPS vers une page d’informations permettant aux administrateurs d’obtenir des instructions avant d’autoriser une application, qui est bloquée par défaut. Il peut également être utilisé pour fournir des instructions ou des informations sur l’application, ce qui peut être utile pour l’administrateur du locataire.

## <a name="subscriptionoffer"></a>subscriptionOffer

**Facultatif**— objet

Spécifie l’offre SaaS associée à votre application.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`offerId`| string | 2 048 caractères | ✔ | Identificateur unique qui inclut votre ID de serveur de publication et votre ID d’offre, que vous pouvez trouver dans [Espace partenaires](https://partner.microsoft.com/dashboard). Vous devez mettre en forme la chaîne en tant que `publisherId.offerId`.|

## <a name="see-also"></a>Voir aussi

* [Comprendre la structure de l’application Microsoft Teams](~/concepts/design/app-structure.md)
* [Activer la personnalisation d’application](~/concepts/design/enable-app-customization.md)
* [Localiser votre application](~/concepts/build-and-test/apps-localization.md)
* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Informations de référence sur le schéma du manifeste de la préversion du développeur - Teams](~/resources/schema/manifest-schema-dev-preview.md)
