---
title: Informations de référence sur le schéma du manifeste de la préversion du développeur public
description: Découvrez l’exemple de fichier manifeste et la description de tous ses composants pris en charge pour Microsoft Teams.
ms.topic: reference
ms.localizationpriority: medium
ms.date: 11/15/2021
ms.openlocfilehash: deaf094ab18ddd2ebe70ea9594f41c108398bf32
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142736"
---
# <a name="reference-public-developer-preview-manifest-schema-for-microsoft-teams"></a>Référence : Schéma de manifeste de la version préliminaire du développeur public pour Microsoft Teams

Pour plus d’informations sur l’activation de la préversion des développeurs, consultez [Aperçu publique des développeurs pour Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).

> [!NOTE]
> Si vous n’utilisez pas les fonctionnalités d’aperçu des développeurs, notamment l’exécution des [Onglets personnels Teams et extensions de message dans Outlook et Office](../../m365-apps/overview.md), utilisez plutôt le manifeste d’[application pour les fonctionnalités de disponibilité générale](~/resources/schema/manifest-schema.md) .

Le manifeste Microsoft Teams décrit comment l’application s’intègre à la plateforme Microsoft Teams. Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .

## <a name="sample-full-manifest"></a>Exemple du manifeste complet

```json
{
    "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion": "devPreview",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "devicePermissions": [
        "geolocation",
        "media"
    ],
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
            "scopes": [
                "team",
                "groupchat"
            ]"context": []
        }
    ],
    "staticTabs": [
        {
            "entityId": "idForPage",
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content?host=msteams",
            "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
            "websiteUrl": "https://contoso.com/content",
            "scopes": [
                "personal"
            ]
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "supportsFiles": true,
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
                            "title": "Command N",
                            "description": "Description of Command N"
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
            "configurationUrl": "https://contoso.com/teamsconnector/configure",
            "scopes": [
                "team"
            ]
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
                    "type": "search",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
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
                    "type": "action",
                    "fetchTask": true,
                    "context": [
                        "message"
                    ],
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
                    "id": "exampleMessageHandler",
                    "title": "Message Handler",
                    "description": "Domains that will create a preview when pasted into the compose box",
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
    "defaultInstallScope": "meetings",
    "defaultGroupCapability": {
        "meetings": "tab",
        "team": "bot",
        "groupchat": "bot"
    },
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

*Facultatif, mais recommandé*&ndash; chaîne

URL `https://` faisant référence au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifestVersion

Chaîne **requise**&ndash;

Version du schéma de manifeste que ce manifeste utilise.

## <a name="version"></a>version

Chaîne **requise**&ndash;

Version de l’application spécifique. Si vous mettez à jour un élément dans votre manifeste, la version doit également être incrémentée. Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités. Si cette application a été soumise au Store, le nouveau manifeste doit être soumis à nouveau et validé à nouveau. Ensuite, les utilisateurs de cette application recevront automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.

Si les autorisations demandées par l’application changent, les utilisateurs sont invités à mettre à niveau et à donner à nouveau leur consentement à l’application.

Cette chaîne de version doit suivre la norme de [semver](http://semver.org/) (MAJOR. MINOR. PATCH).

## <a name="id"></a>id

**Obligatoire** &ndash; ID d’application Microsoft

Identificateur unique généré par Microsoft pour cette application. Si vous avez inscrit un bot via le Microsoft Bot Framework, ou si l’application web de votre onglet se connecte déjà avec Microsoft, vous devez déjà avoir un ID et l’entrer ici. Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft ([Mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous [ajoutez un bot](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName

Chaîne **requise**&ndash;

Identificateur unique de cette application en notation de domaine inverse ; par exemple, com.example.myapp.

## <a name="developer"></a>developer

Obligatoire :

Spécifie des informations sur votre entreprise. Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔️|Nom complet du développeur.|
|`websiteUrl`|2 048 caractères|✔️|L’URL https:// du site web du développeur. Ce lien doit diriger les utilisateurs vers votre entreprise ou votre page d’accueil spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔️|L’URL https:// vers la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔️|L’URL https:// vers les conditions d’utilisation du développeur.|
|`mpnId`|10 caractères|✔️|**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="localizationinfo"></a>localizationInfo

Facultatif :

Autorise la spécification d’une langue par défaut et les pointeurs vers des fichiers de langue supplémentaires. Consultez [localisation](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`|4 caractères|✔️|Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

Tableau d’objets spécifiant des traductions de langue supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`|4 caractères|✔️|Balise de langue des chaînes dans le fichier fourni.|
|`file`|4 caractères|✔️|Chemin d’accès relatif au fichier .json contenant les chaînes traduites.|

## <a name="name"></a>nom

Obligatoire :

Nom de l’expérience de votre application, affiché à destination des utilisateurs dans l’expérience Teams. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs de `short` et `full` ne doivent pas être les mêmes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔️|Nom d’affichage court de l’application.|
|`full`|100 caractères||Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

Obligatoire :

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations figurant dans votre entrée AppSource.

Assurez-vous que votre description décrit avec précision votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience. Notez également, dans la description complète, si un compte externe est requis pour être utilisé. Les valeurs de `short` et `full` ne doivent pas être les mêmes.  Votre brève description ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔️|Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4 000 caractères|✔️|Description complète de votre application.|

## <a name="icons"></a>icons

Obligatoire :

Icônes utilisées dans l’application Teams. Les fichiers d’icône doivent être inclus dans le package de chargement.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|2 048 caractères|✔️|Chemin d’accès relatif à un plan PNG transparent 32 x 32.|
|`color`|2 048 caractères|✔️|Chemin d’accès relatif à une icône PNG couleur 192 x 192.|

## <a name="accentcolor"></a>accentColor

Chaîne **requise**&ndash;

Couleur à utiliser avec et comme arrière-plan pour vos icônes de contour.

La valeur doit être un code de couleur HTML valide commençant par « # » par exemple `#4464ee`.

## <a name="configurabletabs"></a>configurableTabs

Facultatif :

Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables sont pris en charge uniquement dans l’étendue Teams, et actuellement, un seul onglet par application est pris en charge.

L’objet est un tableau avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet de canal configurable.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔️|L’URL https:// à utiliser lors de la configuration de l’onglet.|
|`canUpdateConfiguration`|Booléen|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Par défaut : `true`|
|`scopes`|Tableau de l’énum|1|✔️|Actuellement, les onglets configurables ne prennent en charge que les étendues `team` et `groupchat`. |
|`context` |tableau d’énumération|6 ||L’ensemble des `contextItem` étendues où un [onglet est pris en charge](../../tabs/how-to/access-teams-context.md). Par défaut : `channelTab`, `privateChatTab`, `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` et `meetingStage`.|
|`sharePointPreviewImage`|Chaîne|2048||Un chemin de fichier relatif vers une image d'aperçu d'onglet à utiliser dans SharePoint. Taille 1024x768. |
|`supportedSharePointHosts`|Tableau de l’énum|1||Définit la façon dont votre onglet sera mis à disposition dans SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

Facultatif :

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.

Affichez les onglets avec Cartes adaptatives en spécifiant `contentBotId` au lieu de `contentUrl` dans le bloc **staticTabs**.

L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|String|64 caractères|✔️|Identificateur unique de l’entité affichée par l’onglet.|
|`name`|Chaîne|128 caractères|✔️|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|Chaîne|2 048 caractères|✔️|L’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de canevas de Teams.|
|`contentBotId`|   | | | ID d’application Microsoft Teams spécifié pour le bot dans le portail Bot Framework. |
|`websiteUrl`|Chaîne|2 048 caractères||URL https:// vers laquelle pointer si un utilisateur choisit d’afficher dans un navigateur.|
|`scopes`|Tableau de l’énum|1|✔️|Actuellement, les onglets statiques ne peuvent prendre en charge que `personal` l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.|

## <a name="bots"></a>bots

Facultatif :

Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.

L’objet est un tableau (au maximum 1 élément&mdash;actuellement un seul bot est autorisé par application) avec tous les éléments du type `object`. Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64 caractères|✔️|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela peut être identique à l’[ID d’application](#id) global.|
|`needsChannelSelector`|Booléen|||Indique si le bot utilise ou non un indicateur utilisateur pour ajouter le bot à un canal spécifique. Par défaut : `false`|
|`isNotificationOnly`|Booléen|||Indique si un bot est un bot unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. Par défaut : `false`|
|`supportsFiles`|Booléen|||Indique si le bot prend en charge la possibilité de charger/télécharger des fichiers dans le chat personnel. Par défaut : `false`|
|`scopes`|Tableau de l’énum|3|✔️|Spécifie si le bot offre une expérience dans le contexte d'un canal dans un`team` , dans un chat de groupe (`groupchat` ), ou une expérience scopée à un utilisateur individuel seul (`personal` ). Ces options sont non exclusives.|

### <a name="botscommandlists"></a>bots.commandLists

Liste facultative de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (2 éléments maximum) avec tous les éléments de type `object`; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot. Pour plus d’informations, consultez [Menus bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau de l’énum|3|✔️|Spécifie l'étendue pour laquelle la liste de commandes est valide. Les options sont`team` ,`personal` , et`groupchat`.|
|`items.commands`|tableau d’objets|10|✔️|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande du bot (chaîne, 32).<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

## <a name="connectors"></a>connecteurs

Facultatif :

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum 1 élément) avec tous les éléments de type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔️|L’URL https:// à utiliser lors de la configuration du connecteur.|
|`connectorId`|String|64 caractères|✔️|Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)|
|`scopes`|Tableau de l’énum|1|✔️|Indique si le connecteur offre une expérience dans le contexte d'un canal dans un `team`, ou une expérience limitée à un utilisateur individuel uniquement (`personal` ). Actuellement, seule la `team`portée est prise en charge.|

## <a name="composeextensions"></a>composeExtensions

Facultatif :

Définit une extension de message pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité est passé de « extension composée  » à « extension de message » en novembre 2017, mais le nom du manifeste reste le même afin que les extensions existantes continuent de fonctionner.

L’objet est un tableau (maximum 1 élément) avec tous les éléments de type `object`. Ce bloc est requis uniquement pour les solutions qui fournissent une extension de message.

|Nom| Type | Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|Chaîne|64|✔️|ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de message, tel qu’il est inscrit auprès de l’infrastructure de bot. Cela peut être identique à l’[ID d’application](#id) global.|
|`canUpdateConfiguration`|Booléen|||Valeur indiquant si la configuration d’une extension de message peut être mise à jour par l’utilisateur. La valeur par défaut est `false`.|
|`commands`|Tableau d’objets|10|✔️|Tableau de commandes prises en charge par l’extension de message|

### <a name="composeextensionscommands"></a>composeExtensions.commands

Votre extension de message doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft Teams en tant qu’interaction potentielle à partir du point d’entrée basé sur l’IU. Il y a un maximum de 10 commandes.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|64 caractères|✔️|ID de la commande.|
|`type`|String|64 caractères||Type de la commande. L’un des `query` ou `action`. Par défaut : `query`|
|`title`|Chaîne|32 caractères|✔️|Le nom de la commande conviviale.|
|`description`|Chaîne|128 caractères||Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.|
|`initialRun`|Boolean|||Valeur booléenne qui indique si la commande doit être exécutée initialement sans paramètres. Par défaut : `false`|
|`context`|Tableau de chaînes|3||Définit l’emplacement à partir duquel l’extension de message peut être appelée. Toute combinaison de `compose`, `commandBox`, `message`. La valeur par défaut est `["compose", "commandBox"]`.|
|`fetchTask`|Booléen|||Valeur booléenne qui indique si le module de tâche doit être extrait dynamiquement.|
|`taskInfo`|Objet|||Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de message.|
|`taskInfo.title`|Chaîne|64||Titre de la boîte de dialogue initiale.|
|`taskInfo.width`|Chaîne|||Largeur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.height`|Chaîne|||Hauteur de la boîte de dialogue : un nombre en pixels ou une disposition par défaut telle que « grand », « moyen » ou « petit ».|
|`taskInfo.url`|Chaîne|||URL webview initiale.|
|`messageHandlers`|Tableau d’objets|5||Liste des gestionnaires qui permettent d’appeler des applications lorsque certaines conditions sont remplies. Les domaines doivent également être répertoriés dans `validDomains`.|
|`messageHandlers.type`|Chaîne|||Le type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|Tableau de chaînes|||Tableau de domaines pour lequel le gestionnaire de messages de lien peut s’inscrire.|
|`parameters`|Tableau d’objets|5|✔️|Liste des paramètres que prend la commande. Minimum : 1 ; maximum : 5|
|`parameter.name`|String|64 caractères|✔️|Nom du paramètre tel qu’il apparaît dans le client. Cela est inclus dans la demande de l’utilisateur.|
|`parameter.title`|Chaîne|32 caractères|✔️|Titre convivial du paramètre.|
|`parameter.description`|Chaîne|128 caractères||Chaîne conviviale qui décrit l’objectif de ce paramètre.|
|`parameter.inputType`|Chaîne|128 caractères||Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true`. L’un des `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.|
|`parameter.choices`|Tableau d’objets|10||Options de choix pour le `choiceset`. Utilisez uniquement lorsque `parameter.inputType` est `choiceset`.|
|`parameter.choices.title`|Chaîne|128||Titre du choix.|
|`parameter.choices.value`|Chaîne|512||Valeur du choix.|

## <a name="permissions"></a>autorisations

Facultatif :

Tableau de `string`, qui spécifie les autorisations demandées par l’application, qui permettent aux utilisateurs finaux de savoir comment l’extension s’exécutera. Les options suivantes ne sont pas exclusives :

* `identity` &emsp;Nécessite des informations d’identité d’utilisateur.
* `messageTeamMembers` &emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.

Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répètent le processus de consentement la première fois qu’ils exécutent l’application mise à jour.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** Tableau de chaînes

Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auxquels votre application peut demander l’accès. Les options sont les suivantes :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**Facultatif**, sauf **Obligatoire** lorsque indiqué.

Liste des domaines valides à partir desquels l’application s’attend à charger tout contenu. Les listes de domaines peuvent inclure des caractères génériques, par exemple `*.example.com`. Cela correspond exactement à un segment du domaine, si vous devez faire correspondre `a.b.example.com` utilisez `*.*.example.com`. Si la configuration de votre onglet ou l’interface utilisateur du contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration de tabulation, ce domaine doit être spécifié ici.

Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]`.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string`.

## <a name="webapplicationinfo"></a>WebApplicationInfo

Facultatif :

Spécifiez votre ID d’application Microsoft Azure Active Directory (Azure AD) et Graph informations pour aider les utilisateurs à se connecter en toute transparence à votre application Azure AD.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|Chaîne|36 caractères|✔️|ID de l'application Microsoft Azure Active Directory (Azure AD). Cet ID doit être un GUID.|
|`resource`|Chaîne|2 048 caractères|✔️|URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.|
|`applicationPermissions`|Tableau|100 éléments maximum|✔️|Autorisations de ressource pour l’application.|

## <a name="graphconnector"></a>graphConnector

**Facultatif**— objet

Spécifiez la configuration du connecteur Graph de l’application. Si cette valeur est présente, alors [webApplicationInfo.id](#webapplicationinfo) doit également être spécifié.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`notificationUrl`|string|2 048 caractères|✔️|L’URL où les notifications Graph-connecteur pour l’application doivent être envoyées.|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Facultatif**— booléen

Indique si l’indicateur de chargement doit être affiché ou non lors du chargement d’une application ou d’un onglet. La valeur par défaut est **False**.
> [!NOTE]
> Si vous sélectionnez`showLoadingIndicator` comme true dans le manifeste de votre application, pour charger correctement la page, modifiez les pages de contenu de vos onglets et modules de tâches, comme décrit dans le document [Afficher un indicateur de chargement natif](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator).

## <a name="isfullscreen"></a>IsFullScreen

 **Facultatif**— booléen

Indique si une application personnelle est rendue avec ou sans barre d'en-tête d'onglet. La valeur par défaut est **faux**.

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
|`type`|string|32 caractères|✔️|Le type de notification. *Voir ci-dessous*.|
|`description`|string|128 caractères|✔️|Une brève description de la notification. *Voir ci-dessous*.|
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

## <a name="configurableproperties"></a>configurableProperties

**Facultatif**— tableau

Le bloc `configurableProperties` définit les propriétés d’application que les administrateurs Teams peuvent personnaliser. Pour plus d’informations, consultez [activer la personnalisation d’application](~/concepts/design/enable-app-customization.md).

> [!NOTE]
> Au moins une propriété doit être définie. Vous pouvez définir un maximum de neuf propriétés dans ce bloc.

Vous pouvez définir l’une des propriétés suivantes :

* `name` : Nom d’affichage de l’application.
* `shortDescription` : Description courte de l’application.
* `longDescription` : description détaillée de l’application.
* `smallImageUrl` : Icône de contour de l’application.
* `largeImageUrl` : Icône de couleur de l’application.
* `accentColor`: couleur à utiliser avec et comme arrière-plan pour vos icônes de contour.
* `developerUrl` : URL HTTPS du site web du développeur.
* `privacyUrl` : URL HTTPS de la politique de confidentialité du développeur.
* `termsOfUseUrl` : URL HTTPS des conditions d’utilisation du développeur.

## <a name="defaultinstallscope"></a>defaultInstallScope

**Facultatif**— chaîne

Spécifie l’étendue d’installation définie par défaut pour cette application. L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application. Les options sont :

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**Facultatif**— objet

Lorsqu'un champ d'installation de groupe est sélectionné, il définit la capacité par défaut lorsque l'utilisateur installe l'application. Les options sont les suivantes :

* `team`
* `groupchat`
* `meetings`

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`team`|string|||Lorsque l'étendue de l'installation sélectionnée est `team`, ce champ indique la capacité par défaut disponible. Options : `tab``bot`, , ou`connector` .|
|`groupchat`|string|||Lorsque l'étendue de l'installation sélectionnée est `groupchat`, ce champ indique la capacité par défaut disponible. Options : `tab`, `bot`, ou `connector`.|
|`meetings`|string|||Lorsque l'étendue de l'installation sélectionnée est `meetings`, ce champ indique la capacité par défaut disponible. Options : `tab``bot`, , ou`connector` .|

## <a name="subscriptionoffer"></a>subscriptionOffer

**Facultatif**— objet

Spécifie l’offre SaaS associée à votre application.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`offerId`| string | 2 048 caractères | ✔️ | Un identifiant unique qui comprend votre ID d'éditeur et votre ID d'offre, que vous pouvez trouver dans le [centre des partenaires](https://partner.microsoft.com/dashboard). Vous devez formater la chaîne de caractères comme suit`publisherId.offerId`|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**Facultatif**— objet

Spécifiez la définition de l'extension de réunion. Pour plus d'informations, voir [les scènes personnalisées en mode Ensemble dans Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`scenes`|tableau d’objets| 5 éléments||Scènes de réunion prise en charge.|

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
|`type`|string||✔️| Le type de l'autorisation spécifique à la ressource. Options : `Application`et `Delegated`.|
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

* **Autorisations déléguées spécifiques aux ressources pour les conversations ou les réunions**

    |**Name**|**Description**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|Permet à l’application d’afficher les offres Marketplace aux utilisateurs de cette conversation, ainsi que toute réunion associée, et d’effectuer leurs achats au sein de l’application, au nom de l’utilisateur connecté.|
    |`MeetingStage.Write.Chat`|Permet à l’application d’afficher du contenu sur la phase de réunion dans les réunions associées à cette conversation, au nom de l’utilisateur connecté.|
    |`OnlineMeetingParticipant.Read.Chat`|Permet à l’application de lire les informations des participants, y compris le nom, le rôle, l’ID, les heures de participation et les heures restantes, de la réunion associée à cette conversation, au nom de l’utilisateur.|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|Permet à l’application de basculer l’audio entrant pour les participants aux réunions associées à cette conversation, pour le compte de l’utilisateur connecté.|

* **Autorisations déléguées spécifiques aux ressources pour les utilisateurs**

    |**Name**|**Description**|
    |---|---|
    |`InAppPurchase.Allow.User`|Permet à l’application d’afficher les offres marketplace de l’utilisateur et d’effectuer les achats de l’utilisateur au sein de l’application, au nom de l’utilisateur connecté.|

* **Autorisations spécifiques aux ressources pour Teams partage en direct**

   |Nom| Description |
   | ----- | ----- |
   |`LiveShareSession.ReadWrite.Chat`|<!--- need info --->|
   |`LiveShareSession.ReadWrite.Channel`|<!--- need info --->|
   |`MeetingStage.Write.Chat`|<!--- need info --->|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|<!--- need info --->|

## <a name="see-also"></a>Voir aussi

* [Comprendre la structure de l’application Microsoft Teams](~/concepts/design/app-structure.md)
* [Activer la personnalisation d’application](~/concepts/design/enable-app-customization.md)
* [Localiser votre application](~/concepts/build-and-test/apps-localization.md)
* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/media-capabilities.md)
