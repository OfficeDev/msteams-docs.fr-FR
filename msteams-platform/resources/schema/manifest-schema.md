---
title: Référence du schéma du manifeste
description: Dans cet article, vous trouverez la dernière version du schéma de manifeste public pour la référence, le schéma et l’exemple de manifeste complet de Microsoft Teams.
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 2638c668bf1363a0f997786bcb958689626c70c6
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499173"
---
# <a name="app-manifest-schema-for-teams"></a>Schéma du manifeste d’application pour Teams

Le manifeste de l’application Microsoft Teams décrit comment votre application s’intègre au produit Microsoft Teams. Votre manifeste d’application doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json) . Les versions précédentes 1.0, 1.1,...,1.13 et la version actuelle 1.14 sont toutes prises en charge (à l’aide de « v1.x » dans l’URL).
Pour plus d’informations sur les modifications apportées dans chaque version, voir [le journal des modifications du manifeste.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)

Le tableau suivant répertorie les versions teamsJS et les versions du manifeste d’application en fonction des différents scénarios d’application :

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

L’exemple de schéma suivant montre toutes les options d’extensibilité :

## <a name="sample-full-manifest"></a>Exemple du manifeste complet

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json",
    "manifestVersion": "1.14",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
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
            "context": [
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
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
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
                    "fetchTask": false ,
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
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
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
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

Chaîne facultative, mais recommandée

L’URL https:// fait référence au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifestVersion

**Obligatoire**— chaîne

La version du schéma de manifeste que ce manifeste utilise. Utilisez `1.13` pour activer la prise en charge des applications Teams dans Outlook et Office; utilisez `1.12` (ou avant) pour les applications Teams uniquement.

## <a name="version"></a>version

**Obligatoire**— chaîne

Version d’une application spécifique. Lorsque vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée. De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité. Lorsque cette application a été soumise à Store, le nouveau manifeste doit être soumis à nouveau et revalidé. Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.

Si l’application demande le changement des autorisations, les utilisateurs sont invités à mettre à niveau et à se réinscrire à l’application.

Cette chaîne de version doit suivre la norme de [semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>ID

**Obligatoire** — ID d’application Microsoft

L’ID est un identificateur unique généré par Microsoft pour l’application. Vous avez un ID si votre bot est inscrit via le Microsoft Bot Framework. Vous avez un ID si l’application web de votre onglet se signe déjà avec Microsoft. Vous devez entrer l’ID ici. Sinon, vous devez générer un nouvel ID sur le [portail d’inscription des applications Microsoft.](https://aka.ms/appregistrations) Utilisez le même ID si vous ajoutez un bot.

> [!NOTE]
> Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.

## <a name="developer"></a>developer

**Obligatoire**— objet

Spécifie des informations sur votre entreprise. Pour les applications soumises au magasin Teams, ces valeurs doivent correspondre aux informations figurant dans votre description du magasin. Pour plus d’informations, voir les [instructions pour la publication dans les magasins Teams](~/concepts/deploy-and-publish/appsource/publish.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔️|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔️|L’URL https:// du site web du développeur. Ce lien doit conduire les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔️|L’URL https:// vers la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔️|L’URL https:// vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères| |**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="name"></a>nom

**Obligatoire**— objet

Nom de l’expérience de votre application, affiché à destination des utilisateurs dans l’expérience Teams. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs de `short` et `full` doivent être différentes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔️|Nom d’affichage court de l’application.|
|`full`|100 caractères||Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Obligatoire**— objet

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrive votre expérience et aide les clients potentiels à comprendre ce que fait votre expérience. Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé. Les valeurs de `short` et `full` doivent être différentes. Votre brève description ne peut pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔️|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4 000 caractères|✔️|Description complète de votre application.|

## <a name="localizationinfo"></a>localizationInfo

**Facultatif**— objet

Allows the specification of a default language and provides pointers to more language files. For more information, see [localization](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`||✔️|La balise de langue des chaînes dans ce fichier du manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant davantage de traductions linguistiques.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`||✔️|Balise de langue des chaînes dans le fichier fourni.|
|`file`||✔️|Chemin d’accès relatif au fichier .json contenant les chaînes traduites.|

## <a name="icons"></a>icons

**Obligatoire**— objet

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de chargement. Pour plus d’informations, voir [Icônes](../../concepts/build-and-test/apps-package.md#app-icons).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|32 x 32 pixels|✔️|Chemin d’accès relatif à un plan PNG transparent 32 x 32.|
|`color`|192 x 192 pixels|✔️|Chemin d’accès relatif à une icône PNG couleur 192 x 192.|

## <a name="accentcolor"></a>accentColor

**Obligatoire**— Code de couleur HTML Hex

Couleur à utiliser et en arrière-plan pour vos icônes de plan.

La valeur doit être un code de couleur HTML valide commençant par « # » par exemple `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

**Facultatif**— tableau

Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans les étendues `team` et `groupchat` vous pouvez configurer les mêmes onglets plusieurs fois. Toutefois, vous ne pouvez la définir dans le manifeste qu’une seule fois.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔️|L’URL https:// à utiliser lors de la configuration de l’onglet.|
|`scopes`|tableau d’énumération|1|✔️|Actuellement, les onglets configurables ne prennent en charge que les étendues `team` et `groupchat`. |
|`canUpdateConfiguration`|Boolean|||A value indicating whether an instance of the tab's configuration can be updated by the user after creation. Default: **true**.|
|`context` |tableau d’énumération|6||L’ensemble des `contextItem` étendues où un [onglet est pris en charge](../../tabs/how-to/access-teams-context.md). Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||A relative file path to a tab preview image for use in SharePoint. Size 1024x768. |
|`supportedSharePointHosts`|tableau d’énumération|1||Defines how your tab is made available in SharePoint. Options are `sharePointFullPage` and `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Facultatif**— tableau

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.

Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|string|64 caractères|✔️|Identificateur unique de l’entité affichée par l’onglet.|
|`name`|chaîne|128 caractères|✔️|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|string||✔️|L’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de canevas de Teams.|
|`websiteUrl`|string|||L’URL https:// pointant vers si un utilisateur choisit de l’afficher dans un navigateur.|
|`searchUrl`|chaîne|||L’URL https:// pointant vers les requêtes de recherche d’un utilisateur.|
|`scopes`|tableau d’énumération|1|✔️|Actuellement, les onglets statiques ne peuvent prendre en charge que `personal` l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.|
|`context` | tableau d’énumération| 2|| L’ensemble `contextItem` des étendues où un onglet est pris en charge.|

> [!NOTE]
> The searchUrl feature is not available for the third-party developers.
> If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>bots

**Facultatif**— tableau

Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’élément est un tableau (maximum d’un seul élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` . Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64 caractères|✔️|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. L’ID peut être identique à [l’ID d’application](#id) globale.|
|`scopes`|tableau d’énumération|3|✔️|Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`). These options are non-exclusive.|
|`needsChannelSelector`|Boolean|||Describes whether or not the bot uses a user hint to add the bot to a specific channel. Default: **`false`**|
|`isNotificationOnly`|Booléen|||Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot. Default: **`false`**|
|`supportsFiles`|Booléen|||Indicates whether the bot supports the ability to upload/download files in personal chat. Default: **`false`**|
|`supportsCalling`|Boolean|||Valeur indiquant où un bot prend en charge les appels audio. **IMPORTANT** : Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Par défaut :**`false`**|
|`supportsVideo`|Boolean|||Valeur indiquant où un bot prend en charge les appels vidéo. **IMPORTANT** : Cette propriété est actuellement expérimentale. Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.  La propriété est fournie uniquement à des fins de test et d’exploration et ne doit pas être utilisée dans les applications de production. Par défaut :**`false`**|

### <a name="botscommandlists"></a>bots.commandLists

Une liste de commandes que votre robot peut recommander aux utilisateurs. L’objet est un tableau (maximum de deux éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commandes distincte pour chaque étendue que votre bot prend en charge. Pour plus d’informations, consultez [Menus bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau d’énumération|3|✔️|Specifies the scope for which the command list is valid. Options are `team`, `personal`, and `groupchat`.|
|`items.commands`|tableau d’objets|10|✔️|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|title|string|12 |✔️|Nom de la commande du bot.|
|description|string|128 caractères|✔️|Une description de texte simple ou exemple de syntaxe de commande et de ses arguments.|

## <a name="connectors"></a>connecteurs

**Facultatif**— tableau

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum d’un élément) avec tous les éléments de type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|string|2 048 caractères|✔️|L’URL https:// à utiliser lors de la configuration du connecteur.|
|`scopes`|tableau d’énumération|1|✔️|Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`). Currently, only the `team` scope is supported.|
|`connectorId`|string|64 caractères|✔️|Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)|

## <a name="composeextensions"></a>composeExtensions

**Facultatif**— tableau

Définit une extension de message pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité est passé de « extension composée  » à « extension de message » en novembre 2017, mais le nom du manifeste reste le même afin que les extensions existantes continuent de fonctionner.

L’élément est un tableau (maximum d’un élément) avec tous les éléments de type `object` . Ce bloc est requis uniquement pour les solutions qui fournissent une extension de message.

|Nom| Type | Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|string|64|✔️|ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de message, tel qu’il est inscrit auprès de l’infrastructure de bot. L’ID peut être identique à l’ID d’application global.|
|`commands`|tableau d’objets|10|✔️|Tableau de commandes prises en charge par l’extension de message.|
|`canUpdateConfiguration`|Booléen|||A value indicating whether the configuration of a message extension can be updated by the user. Default: **false**.|
|`messageHandlers`|tableau d’Objets|5||Liste des gestionnaires qui permettent d’appeler des applications lorsque certaines conditions sont remplies.|
|`messageHandlers.type`|string|||The type of message handler. Must be `"link"`.|
|`messageHandlers.value.domains`|tableau de Chaînes|||Tableau de domaines pour lequel le gestionnaire de messages de lien peut s’inscrire.|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Votre extension de message doit déclarer une ou plusieurs commandes avec un maximum de 10 commandes. Chaque commande apparaît dans Microsoft Teams en tant qu’interaction potentielle à partir du point d’entrée basé sur l’IU.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|64 caractères|✔️|ID de la commande.|
|`title`|chaîne|32 caractères|✔️|Le nom de la commande conviviale.|
|`type`|string|64 caractères||Type de la commande. L’un des `query` ou `action`. Par défaut : **requête**.|
|`description`|chaîne|128 caractères||Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.|
|`initialRun`|Boolean|||A Boolean value indicates whether the command runs initially with no parameters. Default is **false**.|
|`context`|tableau de Chaînes|3||Définit l’emplacement à partir duquel l’extension de message peut être appelée. N’importe quelle combinaison de `compose`,`commandBox` ,`message` . La valeur par défaut est `["compose","commandBox"]`.|
|`fetchTask`|Boolean|||A Boolean value that indicates if it must fetch the task module dynamically. Default is **false**.|
|`taskInfo`|objet|||Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de message.|
|`taskInfo.title`|string|64 caractères||Titre de la boîte de dialogue initiale.|
|`taskInfo.width`|chaîne|||Largeur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.height`|string|||Hauteur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.url`|chaîne|||URL webview initiale.|
|`parameters`|tableau d'objet|5 éléments|✔️|Liste des paramètres que prend la commande. Minimum : 1 ; maximum : 5.|
|`parameters.name`|string|64 caractères|✔️|The name of the parameter as it appears in the client. The parameter name is included in the user request.|
|`parameters.title`|chaîne|32 caractères|✔️|Titre convivial du paramètre.|
|`parameters.description`|string|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameters.value`|string|512 caractères||Valeur initiale du paramètre. Actuellement, la valeur n’est pas prise en charge|
|`parameters.inputType`|chaîne|128 caractères||Defines the type of control displayed on a task module for`fetchTask: false` . One of `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|tableau d’objets|10 éléments||Options de choix pour le `choiceset`. Utilisez uniquement lorsque `parameter.inputType` est `choiceset`.|
|`parameters.choices.title`|string|128 caractères|✔️|Titre du choix.|
|`parameters.choices.value`|string|512 caractères|✔️|Valeur du choix.|

## <a name="permissions"></a>autorisations

**Facultatif** — tableau de chaînes

An array of `string`, which specifies which permissions the app requests, which let end users know how the extension does. The following options are non-exclusive:

* `identity` &emsp;Nécessite des informations d’identité d’utilisateur.
* `messageTeamMembers` &emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.

Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app. For more information, see [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

> [!NOTE]
> Les autorisations sont désormais déconseillées.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** — tableau de chaînes

Provides the native features on a user's device that your app requests access to. Options are:

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

Fournissez votre ID d’application Azure Active Directory et vos informations de Microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application. Si votre application est inscrite dans Microsoft Azure Active Directory (Azure AD), vous devez fournir l’ID de l’application. Les administrateurs peuvent facilement examiner les autorisations et accorder leur consentement dans le Centre d’administration Teams.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|string|36 caractères|✔️|Application Azure AD ID d’application. Cet ID doit être un GUID.|
|`resource`|string|2 048 caractères|✔️|URL de ressource de l’application pour l’acquisition du jeton du SSO. </br> **NOTE:** Si vous n’utilisez pas l’authentification unique, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, `https://notapplicable` pour éviter une réponse d’erreur. |

## <a name="graphconnector"></a>graphConnector

**Facultatif**— objet

Spécifiez la configuration du connecteur Graph de l’application. Si ce paramètre est présent, [webApplicationInfo.id](#webapplicationinfo) doit également être spécifié.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`notificationUrl`|string|2 048 caractères|✔️|L’URL où les notifications Graph-connecteur pour l’application doivent être envoyées.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Facultatif**— booléen

Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement. La valeur par défaut est **False**.
>[!NOTE]
>Si vous sélectionnez `showLoadingIndicator` true dans le manifeste de votre application, pour charger correctement la page, modifiez les pages de contenu de vos onglets et modules de tâches, comme décrit dans [Afficher un document d’indicateur de chargement natif](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) .

## <a name="isfullscreen"></a>IsFullScreen

 **Facultatif**— booléen

Indique si une application personnelle est rendue sans barre d’en-tête d’onglet (mode plein écran). La valeur par défaut est **False**.

> [!NOTE]
>
> * `isFullScreen` ne fonctionne que pour les applications publiées dans votre organisation. Les applications tierces intégrées et publiées ne peuvent pas utiliser cette propriété (elle est ignorée).
>
> * `isFullScreen=true` supprime la barre d'en-tête et le titre fournis par Teams des applications personnelles et des boîtes de dialogue du module de tâches.

## <a name="activities"></a>activités

**Facultatif**— objet

Définissez les propriétés utilisées par votre application pour publier un flux d’activité utilisateur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`activityTypes`|tableau d’Objets|128 éléments| | Indiquez les types d’activités que votre application peut publier dans un flux d’activités utilisateurs.|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`type`|string|32 caractères|✔️|Le type de notification. *Voir ci-dessous*.|
|`description`|string|128 caractères|✔️|A brief description of the notification. *See below*.|
|`templateText`|string|128 caractères|✔️|Exemple : « {actor} a créé la tâche {taskId} pour vous »|

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

When a group install scope is selected, it will define the default capability when the user installs the app. Options are:

* `team`
* `groupchat`
* `meetings`

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`team`|string|||When the install scope selected is `team`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`groupchat`|string|||When the install scope selected is `groupchat`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`meetings`|string|||When the install scope selected is `meetings`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|

## <a name="configurableproperties"></a>configurableProperties

**Facultatif**— tableau

Le bloc `configurableProperties` définit les propriétés d’application que les administrateurs Teams peuvent personnaliser. Pour plus d’informations, consultez [activer la personnalisation d’application](~/concepts/design/enable-app-customization.md). La fonctionnalité de personnalisation d’application n’est pas prise en charge dans les applications personnalisées ou LOB.

> [!NOTE]
> Au moins une propriété doit être définie. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.

Vous pouvez définir l’une des propriétés suivantes :

* [nom](#name) : nom complet de l’application.
* [shortDescription](#description) : description courte de l’application.
* [longDescription](#description) : description longue de l’application.
* [smallImageUrl](#icons) : icône de contour de l’application.
* [largeImageUrl](#icons) : icône de couleur de l’application.
* [accentColor](#accentcolor) : couleur à utiliser et arrière-plan pour vos icônes de contour.
* [developerUrl](#developer) : URL HTTPS du site web du développeur.
* [privacyUrl](#developer) : URL HTTPS de la politique de confidentialité du développeur.
* [termsOfUseUrl](#developer) : URL HTTPS des conditions d’utilisation du développeur.

## <a name="supportedchanneltypes"></a>supportedChannelTypes

**Facultatif**— tableau

Active votre application dans des canaux non standard. Si votre application prend en charge une étendue d’équipe et que cette propriété est définie, Teams active votre application dans chaque type de canal en conséquence. Actuellement, les types de canaux privés et partagés sont pris en charge.

> [!NOTE]
>
> * Si votre application prend en charge une étendue d’équipe, elle fonctionne dans les canaux standard, quelles que soient les valeurs définies dans cette propriété.
> * Votre application peut prendre en compte les propriétés uniques de chacun des types de canaux pour fonctionner correctement. Pour activer votre onglet pour les canaux privés et partagés, consultez [récupérer le contexte dans les canaux privés](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) et [obtenir le contexte dans les canaux partagés](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**Facultatif** - Booléen

Lorsque la propriété `defaultBlockUntilAdminAction` est définie sur **true**, l’application est masquée par défaut aux utilisateurs jusqu’à ce que l’administrateur l’autorise. Si la valeur est **true**, l’application est masquée pour tous les locataires et tous les utilisateurs finaux. Les administrateurs de locataire peuvent voir l’application dans le Centre d’administration Teams et prendre des mesures pour autoriser ou bloquer l’application. La valeur par défaut est **false**. Pour plus d’informations sur le bloc d’application par défaut, consultez [Bloquer les applications par défaut pour les utilisateurs jusqu’à ce qu’un administrateur approuve](../../concepts/design/enable-app-customization.md#block-apps-by-default-for-users-until-an-admin-approves)

## <a name="publisherdocsurl"></a>publisherDocsUrl

**Facultatif**— chaîne

**Maille maximale** — 128 caractères

Le `publisherDocsUrl` est une URL HTTPS vers une page d’informations permettant aux administrateurs d’obtenir des instructions avant d’autoriser une application, qui est bloquée par défaut. Il peut également être utilisé pour fournir des instructions ou des informations sur l’application, ce qui peut être utile pour l’administrateur du locataire.

## <a name="subscriptionoffer"></a>subscriptionOffer

**Facultatif**— objet

Spécifie l’offre SaaS associée à votre application.

|Nom| Type|Taille maximale|Requis|Description|
|---|---|---|---|---|
|`offerId`| string | 2 048 caractères | ✔️ | A unique identifier that includes your Publisher ID and Offer ID, which you can find in [Partner Center](https://partner.microsoft.com/dashboard). You must format the string as `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**Facultatif**— objet

Specify meeting extension definition. For more information, see [custom Together Mode scenes in Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`scenes`|tableau d’objets| 5 éléments||Scènes de réunion prise en charge.|
|`supportsStreaming`|Boolean|||Valeur qui indique si une application peut diffuser en continu le contenu audio et vidéo de la réunion vers un point de terminaison RTMP (Real-Time Meeting Protocol). La valeur par défaut est **false**.|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|Nom| Type|Taille maximale|Requis |Description|
|---|---|---|---|---|
|`id`|||✔️| Identificateur unique de la scène. Cet ID doit être un GUID. |
|`name`| string | 128 caractères |✔️| Nom de la scène. |
|`file`|||✔️| Chemin d’accès relatif au fichier json de métadonnées des scènes. |
|`preview`|||✔️| Chemin d’accès relatif au fichier de l’icône d’aperçu PNG des scènes. |
|`maxAudience`| entier | 50  |✔️| Nombre maximal d’audiences pris en charge dans la scène. |
|`seatsReservedForOrganizersOrPresenters`| entier | 50 |✔️| Nombre de sièges réservés aux organisateurs ou présentateurs.|

## <a name="authorization"></a>autorisation

**Facultatif**— objet

> [!NOTE]
> If you set the `manifestVersion` property to 1.12, the authorization property is incompatible with the older versions (version 1.11 or earlier) of the manifest. Authorization is supported for manifest version 1.12.

Spécifiez et consolidez les informations relatives à l’autorisation pour l’application.

|Nom| Type|Taille maximale|Requis |Description|
|---|---|---|---|---|
|`permissions`||||Liste des autorisations dont l’application a besoin pour fonctionner.|

### <a name="authorizationpermissions"></a>authorization.permissions

|Nom| Type|Taille maximale|Requis |Description|
|---|---|---|---|---|
|`resourceSpecific`| tableau d’objets|16 éléments||Autorisations qui protègent l’accès aux données au niveau de l’instance de ressource.|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|Nom| Type|Taille maximale|Requis |Description|
|---|---|---|---|---|
|`type`|string||✔️| The type of the resource-specific permission. Options: `Application` and `Delegated`.|
|`name`|string|128 caractères|✔️|Nom de l’autorisation spécifique à la ressource. Pour plus d’informations, consultez [Autorisations d'application spécifiques aux ressources](#resource-specific-application-permissions) et [Autorisations déléguées spécifiques aux ressources](#resource-specific-delegated-permissions)|

#### <a name="resource-specific-application-permissions"></a>Autorisations d’application spécifiques aux ressources

Les autorisations d’application permettent à l’application d’accéder aux données sans utilisateur connecté. Pour plus d’informations sur les autorisations d’application, consultez [Consentement spécifique aux ressources pour MS Graph et MS BotSDK](../../graph-api/rsc/resource-specific-consent.md).

#### <a name="resource-specific-delegated-permissions"></a>Autorisations déléguées spécifiques aux ressources

Les autorisations déléguées permettent à l’application d’accéder aux données pour le compte de l’utilisateur.

* **Autorisations déléguées spécifiques aux ressources pour les équipes**

    |**Name**|**Description**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| Permet à l’application de lire les informations des participants, notamment le nom, le rôle, l’ID, les horaires de participation et le temps restant, des réunions de canal associées à cette équipe, au nom de l’utilisateur connecté.|
    |`InAppPurchase.Allow.Group`| Permet à l’application d’afficher les offres Marketplace aux utilisateurs de cette équipe et d’effectuer leurs achats au sein de l’application, au nom de l’utilisateur connecté.|
    |`ChannelMeetingStage.Write.Group`| Permet à l’application d’afficher du contenu sur la fenêtre de partage des réunions de canal associées à cette équipe, pour le compte de l’utilisateur connecté.|
    |`LiveShareSession.ReadWrite.Group`|Permet à l’application de créer et de synchroniser des sessions Live Share pour les réunions associées à cette équipe, et d’accéder aux informations connexes sur la liste de la réunion, telles que le rôle de réunion du membre, pour le compte de l’utilisateur connecté.|

* **Autorisations déléguées spécifiques aux ressources pour les conversations ou les réunions**

    |**Name**|**Description**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|Permet à l’application d’afficher les offres Marketplace aux utilisateurs de cette conversation, ainsi que toute réunion associée, et d’effectuer leurs achats au sein de l’application, au nom de l’utilisateur connecté.|
    |`MeetingStage.Write.Chat`|Permet à l’application d’afficher du contenu sur la phase de réunion dans les réunions associées à cette conversation, au nom de l’utilisateur connecté.|
    |`OnlineMeetingParticipant.Read.Chat`|Permet à l’application de lire les informations des participants, y compris le nom, le rôle, l’ID, les heures de participation et les heures restantes, de la réunion associée à cette conversation, au nom de l’utilisateur.|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|Permet à l’application de basculer l’audio entrant pour les participants aux réunions associées à cette conversation, pour le compte de l’utilisateur connecté.|
    |`LiveShareSession.ReadWrite.Chat`|Permet à l’application de créer et de synchroniser des sessions Live Share pour les réunions associées à cette conversation, et d’accéder aux informations connexes sur la liste de la réunion, telles que le rôle de réunion du membre, pour le compte de l’utilisateur connecté.|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|Permet à l’application de détecter les modifications apportées à l’état de l’audio entrant dans les réunions associées à cette conversation, pour le compte de l’utilisateur connecté.|

* **Autorisations déléguées spécifiques aux ressources pour les utilisateurs**

    |**Name**|**Description**|
    |---|---|
    |`InAppPurchase.Allow.User`|Permet à l’application d’afficher les offres marketplace de l’utilisateur et d’effectuer les achats de l’utilisateur au sein de l’application, au nom de l’utilisateur connecté.|

## <a name="create-a-manifest-file"></a>Créer un fichier manifeste

Si votre application n’a pas de fichier manifeste d’application Teams, vous devez le créer.

Pour créer un fichier manifeste d’application Teams :

1. Utilisez le [exemple de schéma de manifeste](#sample-full-manifest) pour créer un fichier json.
1. Enregistrez-le à la racine de votre dossier de projet en tant que `manifest.json`.

<br>
<details>
<summary>Voici un exemple de schéma de manifeste pour une application d’onglet avec l’authentification unique activée :</summary>
<br>

> [!NOTE]
> L’exemple de contenu du manifeste présenté ici concerne uniquement une application d’onglet. Il utilise des exemples de valeurs pour l’URI de sous-domaine. Pour plus d’informations, consultez [exemple de schéma de manifeste](#sample-full-manifest).

  ```json
{ 
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json", 
 "manifestVersion": "1.12", 
 "version": "1.0.0", 
 "id": "{new GUID for this Teams app - not the Azure AD App ID}", 
 "developer": { 
 "name": "Microsoft", 
 "websiteUrl": "https://www.microsoft.com", 
 "privacyUrl": "https://www.microsoft.com/privacy", 
 "termsOfUseUrl": "https://www.microsoft.com/termsofuse" 
  }, 

  "name": { 
    "short": "Teams Auth SSO", 
    "full": "Teams Auth SSO" 
  }, 


  "description": { 
    "short": "Teams Auth SSO app", 
    "full": "The Teams Auth SSO app" 
  }, 

  "icons": { 
    "outline": "outline.png", 
    "color": "color.png" 
  }, 

  "accentColor": "#60A18E", 
  "staticTabs": [ 
    { 
     "entityId": "auth", 
     "name": "Auth", 
     "contentUrl": "https://https://subdomain.example.com/Home/Index", 
     "scopes": [ "personal" ] 
    } 
  ], 

  "configurableTabs": [ 
    { 
     "configurationUrl": "https://subdomain.example.com/Home/Configure", 
     "canUpdateConfiguration": true, 
     "scopes": [ 
     "team" 
      ] 
    } 
  ], 
  "permissions": [ "identity", "messageTeamMembers" ], 
  "validDomains": [ 
   "{subdomain or ngrok url}" 
  ], 
  "webApplicationInfo": { 
    "id": "{Azure AD AppId}", 
    "resource": "api://subdomain.example.com/{Azure AD AppId}" 
  }
} 
```

</details>

## <a name="see-also"></a>Voir aussi

* [Comprendre la structure de l’application Microsoft Teams](~/concepts/design/app-structure.md)
* [Activer la personnalisation d’application](~/concepts/design/enable-app-customization.md)
* [Localiser votre application](~/concepts/build-and-test/apps-localization.md)
* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/media-capabilities.md)
* [Schéma de manifeste de prévisualisation pour les développeurs publics pour Microsoft Teams](manifest-schema-dev-preview.md)
