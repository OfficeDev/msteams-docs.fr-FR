---
title: Référence manifeste de schéma
description: Décrit le schéma manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: équipes manifestent schéma
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566445"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>Référence: Schéma manifeste pour les Microsoft Teams

Le Teams décrit comment l’application s’intègre dans le Microsoft Teams produit. Votre manifeste doit se conformer au schéma hébergé à [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) . Les versions précédentes 1.0, 1.1,..., 1.6, et ainsi de suite sont également prises en charge (en utilisant « v1.x » dans l’URL).

L’échantillon de schéma suivant montre toutes les options d’extensibilité :

## <a name="sample-full-manifest"></a>Exemple manifeste complet

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
    ],
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
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

Facultatif, mais recommandé — chaîne

L https:// URL faisant référence au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifesteVersion

**Requis** — chaîne

La version du schéma manifeste que ce manifeste utilise. Il doit être 1,10.

## <a name="version"></a>version

**Requis** — chaîne

La version d’une application spécifique. Si vous mettez à jour quelque chose dans votre manifeste, la version doit être incrémentée aussi. De cette façon, lorsque le nouveau manifeste est installé, il l’réécrit et l’utilisateur reçoit la nouvelle fonctionnalité. Si cette application a été soumise au magasin, le nouveau manifeste doit être soumis à nouveau et re-validé. Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour dans les heures qui ont immédiatement après l’approbation du manifeste.

Si les demandes d’autorisations de l’application changent, les utilisateurs sont invités à mettre à niveau et à consentir à nouveau à l’application.

Cette chaîne de version doit suivre la [norme semver](http://semver.org/) (MAJOR. mineur. PATCH).

## <a name="id"></a>id

**Requis** — Id d’application Microsoft

L’ID est un identifiant unique généré par Microsoft pour l’application. Vous avez un IDENTIFIANT si votre bot est enregistré via le Microsoft Bot Framework ou l’application Web de votre onglet se signe déjà avec Microsoft. Vous devez entrer l’iD ici. Sinon, vous devez générer un nouvel ID sur le portail [d’enregistrement des applications Microsoft](https://aka.ms/appregistrations). Utilisez le même ID si vous ajoutez un bot.

> [!NOTE]
> Si vous soumettez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.

## <a name="developer"></a>developer

**Requis** — objet

Spécifie les informations sur votre entreprise. Pour les applications soumises au magasin Teams, ces valeurs doivent correspondre aux informations contenues dans votre annonce de magasin. Pour plus d’informations, consultez les lignes [directrices Teams’édition en magasin.](~/concepts/deploy-and-publish/appsource/publish.md)

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Le nom d’affichage du développeur.|
|`websiteUrl`|2 048 caractères|✔|L https:// URL du site Web du développeur. Ce lien doit emmener les utilisateurs vers votre entreprise ou votre page de destination spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔|Le https:// URL de la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|Le https:// URL aux conditions d’utilisation du développeur.|
|`mpnId`|10 caractères| |**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="name"></a>name

**Requis** — objet

Le nom de votre expérience d’application, affiché aux utilisateurs dans l’expérience Teams’utilisateur. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs et `short` doivent `full` être différentes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Le nom d’affichage court de l’application.|
|`full`|100 caractères||Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Requis** — objet

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrit avec précision votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience. Vous devez noter dans la description complète, si un compte externe est nécessaire pour une utilisation. Les valeurs et `short` doivent `full` être différentes. Votre courte description ne doit pas être répétée dans la longue description et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Une courte description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4000 caractères|✔|La description complète de votre application.|

## <a name="packagename"></a>packageName PackageName PackageName packageName

**Facultatif** — chaîne

Un identificateur unique pour l’application dans la notation de domaine inversé; par exemple, com.example.myapp. Longueur maximale : 64 caractères.

## <a name="localizationinfo"></a>localisationInfo

**Facultatif** — objet

Permet la spécification d’une langue par défaut, ainsi que des pointeurs à des fichiers linguistiques supplémentaires. Pour plus d’informations, [voir localisation](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔|L’étiquette de langue des chaînes dans ce fichier manifeste de haut niveau.|

### <a name="localizationinfoadditionallanguages"></a>localisationInfo.additionalLanguages

Un éventail d’objets spécifier des traductions linguistiques supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`||✔|L’étiquette linguistique des chaînes dans le fichier fourni.|
|`file`||✔|Un chemin de fichier relatif vers un fichier .json contenant les chaînes traduites.|

## <a name="icons"></a>icons

**Requis** — objet

Icônes utilisées dans l’application Teams’application. Les fichiers icônes doivent être inclus dans le paquet de téléchargement. Voir [Icônes pour](../../concepts/build-and-test/apps-package.md#app-icons) plus d’informations.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|32 x 32 pixels|✔|Un chemin de fichier relatif vers une icône transparente de contour PNG 32x32.|
|`color`|192 x 192 pixels|✔|Un chemin de fichier relatif vers une icône PNG 192x192 en couleur.|

## <a name="accentcolor"></a>accentColor

**Facultatif** — Code couleur HTML Hex

Une couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.

La valeur doit être un code couleur HTML valide commençant par '#', par exemple `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Facultatif** — tableau

Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables ne sont pris en charge que dans la portée des équipes et vous pouvez configurer les mêmes onglets plusieurs fois. Toutefois, vous ne pouvez le définir dans le manifeste qu’une seule fois.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|L https:// URL à utiliser lors de la configuration de l’onglet.|
|`scopes`|tableau d’énumérations|1|✔|Actuellement, les onglets configurables ne supportent que `team` les `groupchat` étendues et les étendues. |
|`canUpdateConfiguration`|booléen|||Une valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après la création. Par défaut: **vrai**.|
|`context` |tableau d’énumérations|6 ||L’ensemble des `contextItem` étendues où un [onglet est pris en charge](../../tabs/how-to/access-teams-context.md). Par défaut: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||Un chemin de fichier relatif vers une image d’aperçu d’onglet pour une utilisation SharePoint. Taille 1024x768. |
|`supportedSharePointHosts`|tableau d’énumérations|1||Définit la façon dont votre onglet est disponible en SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs StaticTabs StaticTabs staticTab

**Facultatif** — tableau

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés `personal` dans la portée sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans la `team` portée ne sont actuellement pas pris en charge.

Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du `object` type. Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|string|64 caractères|✔|Un identificateur unique pour l’entité que l’onglet affiche.|
|`name`|string|128 caractères|✔|Le nom d’affichage de l’onglet dans l’interface du canal.|
|`contentUrl`|string||✔|L https:// URL qui indique l’interface utilisateur de l’entité à afficher dans la Teams externe.|
|`websiteUrl`|string|||L https:// URL à pointer vers si un utilisateur choisit de voir dans un navigateur.|
|`searchUrl`|string|||L https:// URL à pointer vers les requêtes de recherche d’un utilisateur.|
|`scopes`|tableau d’énumérations|1|✔|Actuellement, les onglets statiques ne supportent que `personal` la portée, ce qui signifie qu’il ne peut être provisionné que dans le cadre de l’expérience personnelle.|
|`context` | tableau d’énumérations| 2|| L’ensemble des `contextItem` étendues où un onglet est pris en charge.|

> [!NOTE]
>  La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.
> Si vos onglets nécessitent des informations dépendantes du contexte pour afficher le contenu pertinent ou pour lancer un flux d’authentification, Pour plus d’informations, [consultez Le contexte de votre Microsoft Teams onglet](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>Bots

**Facultatif** — tableau

Définit une solution bot, ainsi que des informations optionnelles telles que les propriétés de commande par défaut.

L’élément est un tableau (maximum de seulement 1 élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une expérience bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela peut bien être le même que l’ID de [l’application globale](#id).|
|`scopes`|tableau d’énumérations|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|
|`needsChannelSelector`|booléen|||Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique. faire défaut: **`false`**|
|`isNotificationOnly`|booléen|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. faire défaut: **`false`**|
|`supportsFiles`|booléen|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. faire défaut: **`false`**|
|`supportsCalling`|booléen|||Une valeur indiquant où un bot prend en charge l’appel audio. **IMPORTANT**: Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des changements avant d’être pleinement disponibles.  Il n’est fourni qu’à des fins d’essai et d’exploration et ne doit pas être utilisé dans des applications de production. faire défaut: **`false`**|
|`supportsVideo`|booléen|||Une valeur indiquant où un bot prend en charge l’appel vidéo. **IMPORTANT**: Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des changements avant d’être pleinement disponibles.  Il n’est fourni qu’à des fins d’essai et d’exploration et ne doit pas être utilisé dans des applications de production. faire défaut: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists (en)

Une liste optionnelle de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commande distincte pour chaque champ d’application que votre bot prend en charge. Consultez les [menus Bot pour](~/bots/how-to/create-a-bot-commands-menu.md) plus d’informations.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau d’énumérations|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10|✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands (en)

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|title|string|12 |✔|Le nom de commande bot.|
|description|string|128 caractères|✔|Une simple description de texte ou un exemple de la syntaxe de commande et de ses arguments.|

## <a name="connectors"></a>Connecteurs

**Facultatif** — tableau

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔|L https:// URL à utiliser lors de la configuration du connecteur.|
|`scopes`|tableau d’énumérations|1|✔|Précise si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel seul ( `personal` ). Actuellement, seule la portée `team` est prise en charge.|
|`connectorId`|string|64 caractères|✔|Un identificateur unique pour le connecteur qui correspond à son ID dans le tableau de [bord des développeurs de connecteurs](https://aka.ms/connectorsdashboard).|

## <a name="composeextensions"></a>composerExtensions

**Facultatif** — tableau

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été changé de « composer extension » à « extension de messagerie » en Novembre 2017, mais le nom manifeste reste le même de sorte que les extensions existantes continuent de fonctionner.

L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Obligatoire | Description|
|---|---|---|---|---|
|`botId`|string|64|✔|L’iD unique de l’application Microsoft pour le bot qui prend en arrière l’extension de messagerie, tel qu’enregistré avec le Cadre Bot. Cela peut bien être le même que l’ID app globale.|
|`commands`|tableau d’objets|10|✔|Tableau de commandes pris en charge par l’extension de messagerie.|
|`canUpdateConfiguration`|booléen|||Une valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. Par défaut : **false**.|
|`messageHandlers`|tableau d’objets|5 ||Une liste de gestionnaires qui permettent d’invoquer les applications lorsque certaines conditions sont remplies.|
|`messageHandlers.type`|string|||Le type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|tableau de cordes|||Tableau des domaines pour qui le gestionnaire de message de lien peut s’inscrire.|

### <a name="composeextensionscommands"></a>composerExtensions.commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur. Il y a un maximum de 10 commandes.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|64 caractères|✔|L’identification de la commande.|
|`title`|string|32 caractères|✔|Le nom de commande convivial.|
|`type`|string|64 caractères||Type de commande. L’un `query` ou `action` l’autre de ou . Par défaut **: requête**.|
|`description`|string|128 caractères||La description qui apparaît aux utilisateurs pour indiquer le but de cette commande.|
|`initialRun`|booléen|||Une valeur boolean indique si la commande s’exécute initialement sans paramètres. La valeur par défaut est **False**.|
|`context`|tableau de cordes|3||Définit d’où l’extension de message peut être invoquée. Toute combinaison de `compose` , `commandBox` . `message` La valeur par défaut est `["compose","commandBox"]`.|
|`fetchTask`|booléen|||Une valeur boolean qui indique si elle doit aller chercher le module de tâche dynamiquement. La valeur par défaut est **False**.|
|`taskInfo`|objet|||Spécifiez le module de tâches à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.|
|`taskInfo.title`|string|64 caractères||Titre de dialogue initial.|
|`taskInfo.width`|string|||Largeur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».|
|`taskInfo.height`|string|||Hauteur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».|
|`taskInfo.url`|string|||URL webview initiale.|
|`parameters`|tableau d’objets|5 articles|✔|La liste des paramètres de la commande prend. Minimum: 1; maximum: 5.|
|`parameters.name`|string|64 caractères|✔|Le nom du paramètre tel qu’il apparaît dans le client. Ceci est inclus dans la demande de l’utilisateur.|
|`parameters.title`|string|32 caractères|✔|Titre convivial pour le paramètre.|
|`parameters.description`|string|128 caractères||Chaîne conviviale qui décrit le but de ce paramètre.|
|`parameters.value`|string|512 caractères||Valeur initiale pour le paramètre.|
|`parameters.inputType`|string|128 caractères||Définit le type de contrôle affiché sur un module de tâches pour `fetchTask: true` . L’un des `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|tableau d’objets|10 articles||Les options de choix pour le `choiceset` . Utilisez seulement quand `parameter.inputType` est `choiceset` .|
|`parameters.choices.title`|string|128 caractères|✔|Titre du choix.|
|`parameters.choices.value`|string|512 caractères|✔|Valeur du choix.|

## <a name="permissions"></a>autorisations

**Facultatif** — gamme de chaînes

Un tableau de `string` ce qui spécifie les autorisations des demandes d’application, ce qui permet aux utilisateurs finaux de savoir comment l’extension fonctionne. Les options suivantes ne sont pas exclusives :

* `identity`&emsp;Nécessite des informations d’identité utilisateur.
* `messageTeamMembers`&emsp;Nécessite la permission d’envoyer des messages directs aux membres de l’équipe.

La modification de ces autorisations lors de la mise à jour de l’application, provoque vos utilisateurs à répéter le processus de consentement après avoir exécuté l’application mise à jour. Voir Mise [à jour de votre application pour](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) plus d’informations.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** — gamme de chaînes

Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains (en)

**Facultatif,** sauf requis **lorsqu’il** est noté.

Une liste de domaines valides pour les sites Web que l’application s’attend à charger au sein Teams client. Les listes de domaines peuvent inclure des wildcards, par `*.example.com` exemple, . Cela correspond exactement à un segment du domaine; si vous avez besoin de `a.b.example.com` correspondre, puis utiliser `*.*.example.com` . Si votre configuration d’onglet ou interface utilisateur de contenu doit naviguer vers n’importe quel autre domaine en dehors de l’une des utilisations pour la configuration de l’onglet, ce domaine doit être spécifié ici.

Il **n’est** pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour authentifier à l’aide d’un identifiant Google, il est nécessaire de rediriger vers accounts.google.com, cependant, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

Teams applications qui nécessitent que leurs propres URL sharepoint fonctionnent bien, inclut « {teamsitedomain} » dans leur liste de domaine valide.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont hors de votre contrôle, que ce soit directement ou par wildcards. Par exemple, `yourapp.onmicrosoft.com` est valide, cependant, `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Facultatif** — objet

Fournissez à Azure Active Directory d’application (AAD) et aux informations Graph Microsoft pour aider les utilisateurs à se connecter de manière transparente à votre application. Si votre application est enregistrée dans AAD, vous devez fournir l’ID App, afin que les administrateurs puissent facilement examiner les autorisations et accorder le consentement dans Teams d’administration.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|36 caractères|✔|Id d’application AAD de l’application. Cet id doit être un GUID.|
|`resource`|string|2 048 caractères|✔|URL de ressources de l’application pour l’acquisition de jetons auth pour SSO. </br> **REMARQUE:** Si vous n’utilisez pas SSO, assurez-vous d’entrer une valeur de chaîne factice dans ce champ au manifeste de votre application, par exemple, https://notapplicable pour éviter une réponse d’erreur. |
|`applicationPermissions`|tableau de chaînes|128 caractères||Spécifiez [le consentement spécifique de ressource](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)granulaire.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Facultatif** — boolean

Indique s’il y a ou non un indicateur de chargement lorsqu’une application ou un onglet est en train de charger. La valeur par défaut est **False**.
>[!NOTE]
>Si vous `showLoadingIndicator` sélectionnez comme vrai dans le manifeste de votre application, pour charger correctement la page, modifiez les pages de contenu de vos onglets et modules de tâches tels que décrits dans Afficher un document [indicateur de chargement](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) natif.


## <a name="isfullscreen"></a>isFullScreen

 **Facultatif** — boolean

Indiquez où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet. La valeur par défaut est **False**.

## <a name="activities"></a>activités

**Facultatif** — objet

Définissez les propriétés que votre application utilise pour publier un flux d’activité utilisateur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`activityTypes`|tableau d’objets|128 articles| | Fournissez les types d’activités que votre application peut publier sur un flux d’activité des utilisateurs.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`type`|string|32 caractères|✔|Le type de notification. *Voir ci-dessous*.|
|`description`|string|128 caractères|✔|Une brève description de la notification. *Voir ci-dessous*.|
|`templateText`|string|128 caractères|✔|Ex: « {actor} créé tâche {taskId} pour vous »|

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

Spécifie la portée d’installation définie pour cette application par défaut. La portée définie sera l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application. Les options sont :
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability (en)

**Facultatif** - objet

Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la capacité par défaut lorsque l’utilisateur installe l’application. Les options sont :
* `team`
* `groupchat`
* `meetings`
 
|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`team`|string|||Lorsque la portée d’installation sélectionnée `team` est , ce champ spécifie la capacité par défaut disponible. Options: `tab` , , ou `bot` `connector` .|
|`groupchat`|string|||Lorsque la portée d’installation sélectionnée `groupchat` est , ce champ spécifie la capacité par défaut disponible. Options: `tab` , , ou `bot` `connector` .|
|`meetings`|string|||Lorsque la portée d’installation sélectionnée `meetings` est , ce champ spécifie la capacité par défaut disponible. Options: `tab` , , ou `bot` `connector` .|

## <a name="configurableproperties"></a>configurablesProperties

**Facultatif** - tableau

Le `configurableProperties` bloc définit les propriétés de l’application Teams’administrateur peut personnaliser. Pour plus d’informations, [consultez les applications personnalisées dans Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> Un minimum d’une propriété doit être défini. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.
> En tant que meilleure pratique, vous devez fournir des directives de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.

Vous pouvez définir l’une des propriétés suivantes :
* `name`: Permet à l’administrateur de modifier le nom d’affichage de l’application.
* `shortDescription`: Permet à l’administrateur de modifier la courte description de l’application.
* `longDescription`: Permet à l’administrateur de modifier la description détaillée de l’application.
* `smallImageUrl`: C’est `outline` la propriété dans le bloc du `icons` manifeste.
* `largeImageUrl`: C’est `color` la propriété dans le bloc du `icons` manifeste.
* `accentColor`: C’est la couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.
* `websiteUrl`: Il s’agit https://'URL du site Web du développeur.
* `privacyUrl`: Il s’agit https://'URL de la politique de confidentialité du développeur.
* `termsOfUseUrl`: C’est https:// URL aux conditions d’utilisation du développeur.


