---
title: Développeur Preview Manifeste schema référence
description: Décrit le schéma soutenu par le manifeste pour Microsoft Teams
ms.topic: reference
keywords: équipes manifestent schéma Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566704"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Schéma manifeste de manifeste d’aperçu de développeur pour Microsoft Teams

> [!NOTE]
> Consultez [l’aperçu des](~/resources/dev-preview/developer-preview-intro.md) développeurs pour plus d’informations sur le programme et comment vous pouvez vous inscrire.
> Si vous n’utilisez pas l’aperçu du développeur, vous ne devez pas utiliser cette version du manifeste. Voir [Référence : Schéma manifeste pour Microsoft Teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.

Le Microsoft Teams décrit comment l’application s’intègre dans le Microsoft Teams produit. Votre manifeste doit se conformer au schéma hébergé à [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .

Pour plus d’informations sur les fonctionnalités disponibles voir: [Fonctionnalités dans l’aperçu des développeurs publics pour Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).

## <a name="sample-full-manifest"></a>Exemple manifeste complet

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
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

*Facultatif, mais recommandé* &ndash; corde

L https:// URL faisant référence au schéma JSON pour le manifeste.

## <a name="manifestversion"></a>manifesteVersion

**Requis** &ndash; corde

La version du schéma manifeste que ce manifeste utilise. Il devrait être « devPreview ».

## <a name="version"></a>version

**Requis** &ndash; corde

La version de l’application spécifique. Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée. Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités. Si cette application a été soumise au magasin, le nouveau manifeste devra être soumis à nouveau et re-validé. Ensuite, les utilisateurs de cette application recevront automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.

Si l’application a demandé que les autorisations changent, les utilisateurs seront invités à mettre à niveau et à consentir à nouveau à l’application.

Cette chaîne de version doit suivre la [norme semver](http://semver.org/) (MAJOR. mineur. PATCH).

## <a name="id"></a>id

**Requis** &ndash; ID de l’application Microsoft

L’identifiant unique généré par Microsoft pour cette application. Si vous avez enregistré un bot via le Microsoft Bot Framework, ou si l’application Web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un IDENTIFIANT et l’entrer ici. Sinon, vous devez générer un nouvel ID sur le portail d’enregistrement des applications Microsoft ([Mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez [un bot](~/bots/how-to/create-a-bot-for-teams.md).

## <a name="packagename"></a>packageName PackageName PackageName packageName

**Requis** &ndash; corde

Un identificateur unique pour cette application dans la notation de domaine inverse; par exemple, com.example.myapp.

## <a name="developer"></a>developer

**Obligatoire**

Spécifie les informations sur votre entreprise. Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`name`|32 caractères|✔|Le nom d’affichage du développeur.|
|`websiteUrl`|2 048 caractères|✔|L https:// URL du site Web du développeur. Ce lien doit emmener les utilisateurs vers votre entreprise ou votre page de destination spécifique au produit.|
|`privacyUrl`|2 048 caractères|✔|Le https:// URL de la politique de confidentialité du développeur.|
|`termsOfUseUrl`|2 048 caractères|✔|Le https:// URL aux conditions d’utilisation du développeur.|
|`mpnId`|10 caractères|✔|**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.|

## <a name="localizationinfo"></a>localisationInfo

**Optional**

Permet la spécification d’une langue par défaut, ainsi que des pointeurs à des fichiers linguistiques supplémentaires. Voir [localisation](~/concepts/build-and-test/apps-localization.md).

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`defaultLanguageTag`|4 caractères|✔|L’étiquette de langue des chaînes dans ce fichier manifeste de haut niveau.|

### <a name="localizationinfoadditionallanguages"></a>localisationInfo.additionalLanguages

Un éventail d’objets spécifier des traductions linguistiques supplémentaires.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`languageTag`|4 caractères|✔|L’étiquette linguistique des chaînes dans le fichier fourni.|
|`file`|4 caractères|✔|Un chemin de fichier relatif vers un fichier .json contenant les chaînes traduites.|

## <a name="name"></a>name

**Obligatoire**

Le nom de votre expérience d’application, affiché aux utilisateurs dans l’expérience Teams’utilisateur. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource. Les valeurs de `short` et ne devraient pas être les `full` mêmes.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|30 caractères|✔|Le nom d’affichage court de l’application.|
|`full`|100 caractères||Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.|

## <a name="description"></a>description

**Obligatoire**

Décrit votre application aux utilisateurs. Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.

Assurez-vous que votre description décrit avec précision votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience. Vous devez également noter, dans la description complète, si un compte externe est nécessaire pour une utilisation. Les valeurs de `short` et ne devraient pas être les `full` mêmes.  Votre courte description ne doit pas être répétée dans la longue description et ne doit pas inclure d’autre nom d’application.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`short`|80 caractères|✔|Une courte description de l’expérience de votre application, utilisée lorsque l’espace est limité.|
|`full`|4000 caractères|✔|La description complète de votre application.|

## <a name="icons"></a>icons

**Obligatoire**

Icônes utilisées dans l’application Teams’application. Les fichiers icônes doivent être inclus dans le paquet de téléchargement.

|Nom| Taille maximale | Requis | Description|
|---|---|---|---|
|`outline`|2 048 caractères|✔|Un chemin de fichier relatif vers une icône transparente de contour PNG 32x32.|
|`color`|2 048 caractères|✔|Un chemin de fichier relatif vers une icône PNG 192x192 en couleur.|

## <a name="accentcolor"></a>accentColor

**Requis** &ndash; corde

Une couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.

La valeur doit être un code couleur HTML valide commençant par '#', par exemple `#4464ee` .

## <a name="configurabletabs"></a>configurableTabs

**Optional**

Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée. Les onglets configurables ne sont pris en charge que dans la portée des équipes, et actuellement un seul onglet par application est pris en charge.

L’objet est un tableau avec tous les éléments du type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet de canal configurable.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|String|2 048 caractères|✔|L https:// URL à utiliser lors de la configuration de l’onglet.|
|`canUpdateConfiguration`|Valeur booléenne|||Une valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après la création. faire défaut: `true`|
|`scopes`|Tableau de l’énum|1|✔|Actuellement, les onglets configurables ne supportent que `team` les `groupchat` étendues et les étendues. |
|`sharePointPreviewImage`|String|2048||Un chemin de fichier relatif vers une image d’aperçu d’onglet pour une utilisation SharePoint. Taille 1024x768. |
|`supportedSharePointHosts`|Tableau de l’énum|1||Définit comment votre onglet sera disponible en SharePoint. Les options sont `sharePointFullPage` et `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs StaticTabs StaticTabs staticTab

**Optional**

Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement. Les onglets statiques déclarés `personal` dans la portée sont toujours épinglés à l’expérience personnelle de l’application. Les onglets statiques déclarés dans la `team` portée ne sont actuellement pas pris en charge.

L’objet est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet statique.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|String|64 caractères|✔|Un identificateur unique pour l’entité que l’onglet affiche.|
|`name`|String|128 caractères|✔|Le nom d’affichage de l’onglet dans l’interface du canal.|
|`contentUrl`|String|2 048 caractères|✔|L https:// URL qui indique l’interface utilisateur de l’entité à afficher dans la Teams externe.|
|`websiteUrl`|String|2 048 caractères||L https:// URL à pointer si un utilisateur choisit de voir dans un navigateur.|
|`scopes`|Tableau de l’énum|1|✔|Actuellement, les onglets statiques ne supportent que `personal` la portée, ce qui signifie qu’il ne peut être provisionné que dans le cadre de l’expérience personnelle.|

## <a name="bots"></a>Bots

**Optional**

Définit une solution bot, ainsi que des informations optionnelles telles que les propriétés de commande par défaut.

L’objet est un tableau (maximum de seulement 1 élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une expérience bot.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela peut bien être le même que l’ID de [l’application globale](#id).|
|`needsChannelSelector`|Boolean|||Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique. faire défaut: `false`|
|`isNotificationOnly`|Boolean|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. faire défaut: `false`|
|`supportsFiles`|Boolean|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. faire défaut: `false`|
|`scopes`|Tableau de l’énum|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|

### <a name="botscommandlists"></a>bots.commandLists (en)

Une liste optionnelle de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commande distincte pour chaque champ d’application que votre bot prend en charge. Pour plus d’informations, voir [menus Bot](~/bots/how-to/create-a-bot-commands-menu.md).

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau de l’énum|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10|✔|Ensemble de commandes prises en charge par le bot :<br>`title`: le nom de commande bot (chaîne, 32).<br>`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).|

## <a name="connectors"></a>Connecteurs

**Optional**

Le `connectors` bloc définit un connecteur Office 365 pour l’application.

L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent un connecteur.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|String|2 048 caractères|✔|L https:// URL à utiliser lors de la configuration du connecteur.|
|`connectorId`|String|64 caractères|✔|Un identificateur unique pour le connecteur qui correspond à son ID dans le tableau de [bord des développeurs de connecteurs](https://aka.ms/connectorsdashboard).|
|`scopes`|Tableau de l’énum|1|✔|Précise si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel seul ( `personal` ). Actuellement, seule la portée `team` est prise en charge.|

## <a name="composeextensions"></a>composerExtensions

**Optional**

Définit une extension de messagerie pour l’application.

> [!NOTE]
> Le nom de la fonctionnalité a été changé de « composer extension » à « extension de messagerie » en Novembre 2017, mais le nom manifeste reste le même de sorte que les extensions existantes continuent de fonctionner.

L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` . Ce bloc n’est nécessaire que pour les solutions qui fournissent une extension de messagerie.

|Nom| Type | Taille maximale | Obligatoire | Description|
|---|---|---|---|---|
|`botId`|String|64|✔|L’iD unique de l’application Microsoft pour le bot qui prend en arrière l’extension de messagerie, tel qu’enregistré avec le Cadre Bot. Cela peut bien être le même que l’ID de [l’application globale](#id).|
|`canUpdateConfiguration`|Valeur booléenne|||Une valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur. La valeur par défaut est `false`.|
|`commands`|Tableau d’objet|10|✔|Tableau de commandes que l’extension de messagerie prend en charge|

### <a name="composeextensionscommands"></a>composerExtensions.commands

Votre extension de messagerie doit déclarer une ou plusieurs commandes. Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur. Il y a un maximum de 10 commandes.

Chaque élément de commande est un objet avec la structure suivante :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|64 caractères|✔|L’identification de la commande.|
|`type`|String|64 caractères||Type de commande. L’un `query` ou `action` l’autre de ou . faire défaut: `query`|
|`title`|String|32 caractères|✔|Le nom de commande convivial.|
|`description`|String|128 caractères||La description qui apparaît aux utilisateurs pour indiquer le but de cette commande.|
|`initialRun`|Valeur booléenne|||Une valeur Boolean qui indique si la commande doit être exécuté initialement sans paramètres. faire défaut: `false`|
|`context`|Tableau des cordes|3||Définit d’où l’extension de message peut être invoquée. Toute combinaison de `compose` , `commandBox` . `message` Par défaut est `["compose", "commandBox"]`|
|`fetchTask`|Valeur booléenne|||Une valeur boolean qui indique si elle doit aller chercher le module de tâche dynamiquement.|
|`taskInfo`|Objet|||Spécifiez le module de tâches à précharger lors de l’utilisation d’une commande d’extension de messagerie.|
|`taskInfo.title`|String|64||Titre de dialogue initial.|
|`taskInfo.width`|String|||Largeur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».|
|`taskInfo.height`|String|||Hauteur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».|
|`taskInfo.url`|String|||URL webview initiale.|
|`messageHandlers`|Tableau d’objets|5 ||Une liste de gestionnaires qui permettent d’invoquer les applications lorsque certaines conditions sont remplies. Les domaines doivent également être répertoriés dans `validDomains` .|
|`messageHandlers.type`|String|||Le type de gestionnaire de messages. Doit être `"link"`.|
|`messageHandlers.value.domains`|Tableau des cordes|||Tableau des domaines pour qui le gestionnaire de message de lien peut s’inscrire.|
|`parameters`|Tableau d’objet|5 |✔|La liste des paramètres de la commande prend. Minimum: 1; maximum: 5|
|`parameter.name`|String|64 caractères|✔|Le nom du paramètre tel qu’il apparaît dans le client. Ceci est inclus dans la demande de l’utilisateur.|
|`parameter.title`|String|32 caractères|✔|Titre convivial pour le paramètre.|
|`parameter.description`|String|128 caractères||Chaîne conviviale qui décrit le but de ce paramètre.|
|`parameter.inputType`|String|128 caractères||Définit le type de contrôle affiché sur un module de tâches pour `fetchTask: true` . L’un `text` `textarea` `number` d’eux, `date` , , , , `time` `toggle` `choiceset` .|
|`parameter.choices`|Tableau d’objets|10||Les options de choix pour le `choiceset` . Utilisez seulement quand `parameter.inputType` est `choiceset` .|
|`parameter.choices.title`|String|128||Titre du choix.|
|`parameter.choices.value`|String|512||Valeur du choix.|

## <a name="permissions"></a>autorisations

**Optional**

Un tableau de `string` ce qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment l’extension se produira. Les options suivantes ne sont pas exclusives :

* `identity`&emsp;Nécessite des informations d’identité utilisateur.
* `messageTeamMembers`&emsp;Nécessite la permission d’envoyer des messages directs aux membres de l’équipe.

La modification de ces autorisations lors de la mise à jour de votre application fera répéter le processus de consentement à vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.

## <a name="devicepermissions"></a>devicePermissions

**Facultatif** Tableau des cordes

Spécifie les fonctionnalités natives de l’appareil d’un utilisateur à qui votre application peut demander l’accès. Les options sont :

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains (en)

**Facultatif,** sauf requis **lorsqu’il** est noté

Une liste de domaines valides à partir de laquelle l’application s’attend à charger n’importe quel contenu. Les annonces de domaine peuvent inclure des wildcards, par exemple `*.example.com` . Cela correspond exactement à un segment du domaine; si vous avez besoin de `a.b.example.com` correspondre, puis utiliser `*.*.example.com` . Si votre configuration d’onglet ou interface utilisateur de contenu doit naviguer vers n’importe quel autre domaine en dehors de l’une des utilisations pour la configuration de l’onglet, ce domaine doit être spécifié ici.

Il **n’est** toutefois pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour authentifier à l’aide d’un identifiant Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont hors de votre contrôle, que ce soit directement ou via des wildcards. Par exemple, est `yourapp.onmicrosoft.com` valide, mais `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string` .

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Spécifiez votre identifiant d’application AAD Graph informations supplémentaires pour aider les utilisateurs à se connecter de manière transparente à votre application AAD.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`id`|String|36 caractères|✔|Id d’application AAD de l’application. Cet id doit être un GUID.|
|`resource`|String|2 048 caractères|✔|Url de ressources de l’application pour l’acquisition de jetons auth pour SSO.|

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

