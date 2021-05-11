---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: schéma de manifeste teams
ms.openlocfilehash: eeffd97c5cbe62b66cab343bfe650b7f617ce9f2
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304011"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="0edd5-104">Référence : schéma de manifeste pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0edd5-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="0edd5-105">Le Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="0edd5-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="0edd5-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="0edd5-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="0edd5-107">Les versions précédentes 1.0-1.4 sont également pris en charge (à l’aide de « v1.x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="0edd5-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="0edd5-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="0edd5-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="0edd5-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="0edd5-109">Sample full manifest</span></span>

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

<span data-ttu-id="0edd5-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0edd5-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="0edd5-111">$schema</span><span class="sxs-lookup"><span data-stu-id="0edd5-111">$schema</span></span>

<span data-ttu-id="0edd5-112">Chaîne facultative, mais recommandée</span><span class="sxs-lookup"><span data-stu-id="0edd5-112">Optional, but recommended — string</span></span>

<span data-ttu-id="0edd5-113">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="0edd5-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="0edd5-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="0edd5-114">manifestVersion</span></span>

<span data-ttu-id="0edd5-115">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="0edd5-115">**Required** — string</span></span>

<span data-ttu-id="0edd5-116">Version du schéma de manifeste que ce manifeste utilise.</span><span class="sxs-lookup"><span data-stu-id="0edd5-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="0edd5-117">Elle doit être 1,10.</span><span class="sxs-lookup"><span data-stu-id="0edd5-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="0edd5-118">version</span><span class="sxs-lookup"><span data-stu-id="0edd5-118">version</span></span>

<span data-ttu-id="0edd5-119">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="0edd5-119">**Required** — string</span></span>

<span data-ttu-id="0edd5-120">Version d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="0edd5-120">The version of a specific app.</span></span> <span data-ttu-id="0edd5-121">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="0edd5-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="0edd5-122">De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0edd5-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="0edd5-123">Si cette application a été soumise au Store, le nouveau manifeste doit être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="0edd5-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="0edd5-124">Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.</span><span class="sxs-lookup"><span data-stu-id="0edd5-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="0edd5-125">Si l’application demande des autorisations change, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="0edd5-126">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="0edd5-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="0edd5-127">id</span><span class="sxs-lookup"><span data-stu-id="0edd5-127">id</span></span>

<span data-ttu-id="0edd5-128">**Obligatoire** — ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="0edd5-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="0edd5-129">L’ID est un identificateur unique généré par Microsoft pour l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="0edd5-130">Vous avez un ID si votre bot est inscrit via le Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0edd5-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="0edd5-131">Vous devez entrer l’ID ici.</span><span class="sxs-lookup"><span data-stu-id="0edd5-131">You must enter the ID here.</span></span> <span data-ttu-id="0edd5-132">Sinon, vous devez générer un nouvel ID sur le portail d’inscription [des applications Microsoft.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="0edd5-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="0edd5-133">Utilisez le même ID si vous ajoutez un bot.</span><span class="sxs-lookup"><span data-stu-id="0edd5-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="0edd5-134">Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="0edd5-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="0edd5-135">developer</span><span class="sxs-lookup"><span data-stu-id="0edd5-135">developer</span></span>

<span data-ttu-id="0edd5-136">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-136">**Required** — object</span></span>

<span data-ttu-id="0edd5-137">Spécifie des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="0edd5-137">Specifies information about your company.</span></span> <span data-ttu-id="0edd5-138">Pour les applications envoyées au Teams store, ces valeurs doivent correspondre aux informations de votre listing dans le Windows Store.</span><span class="sxs-lookup"><span data-stu-id="0edd5-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="0edd5-139">Pour plus d’informations, voir les Teams [de publication du Store.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="0edd5-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="0edd5-140">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-140">Name</span></span>| <span data-ttu-id="0edd5-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-141">Maximum size</span></span> | <span data-ttu-id="0edd5-142">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-142">Required</span></span> | <span data-ttu-id="0edd5-143">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="0edd5-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-144">32 characters</span></span>|<span data-ttu-id="0edd5-145">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-145">✔</span></span>|<span data-ttu-id="0edd5-146">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="0edd5-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-147">2048 characters</span></span>|<span data-ttu-id="0edd5-148">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-148">✔</span></span>|<span data-ttu-id="0edd5-149">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="0edd5-150">Ce lien doit prendre les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="0edd5-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="0edd5-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-151">2048 characters</span></span>|<span data-ttu-id="0edd5-152">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-152">✔</span></span>|<span data-ttu-id="0edd5-153">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="0edd5-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-154">2048 characters</span></span>|<span data-ttu-id="0edd5-155">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-155">✔</span></span>|<span data-ttu-id="0edd5-156">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="0edd5-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-157">10 characters</span></span>| |<span data-ttu-id="0edd5-158">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="0edd5-159">name</span><span class="sxs-lookup"><span data-stu-id="0edd5-159">name</span></span>

<span data-ttu-id="0edd5-160">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-160">**Required** — object</span></span>

<span data-ttu-id="0edd5-161">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’Teams expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="0edd5-162">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="0edd5-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="0edd5-163">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="0edd5-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="0edd5-164">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-164">Name</span></span>| <span data-ttu-id="0edd5-165">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-165">Maximum size</span></span> | <span data-ttu-id="0edd5-166">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-166">Required</span></span> | <span data-ttu-id="0edd5-167">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0edd5-168">30 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-168">30 characters</span></span>|<span data-ttu-id="0edd5-169">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-169">✔</span></span>|<span data-ttu-id="0edd5-170">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="0edd5-171">100 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-171">100 characters</span></span>||<span data-ttu-id="0edd5-172">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="0edd5-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="0edd5-173">description</span><span class="sxs-lookup"><span data-stu-id="0edd5-173">description</span></span>

<span data-ttu-id="0edd5-174">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-174">**Required** — object</span></span>

<span data-ttu-id="0edd5-175">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0edd5-175">Describes your app to users.</span></span> <span data-ttu-id="0edd5-176">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="0edd5-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="0edd5-177">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="0edd5-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="0edd5-178">Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="0edd5-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="0edd5-179">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="0edd5-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="0edd5-180">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="0edd5-181">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-181">Name</span></span>| <span data-ttu-id="0edd5-182">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-182">Maximum size</span></span> | <span data-ttu-id="0edd5-183">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-183">Required</span></span> | <span data-ttu-id="0edd5-184">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0edd5-185">80 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-185">80 characters</span></span>|<span data-ttu-id="0edd5-186">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-186">✔</span></span>|<span data-ttu-id="0edd5-187">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="0edd5-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="0edd5-188">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-188">4000 characters</span></span>|<span data-ttu-id="0edd5-189">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-189">✔</span></span>|<span data-ttu-id="0edd5-190">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="0edd5-191">packageName</span><span class="sxs-lookup"><span data-stu-id="0edd5-191">packageName</span></span>

<span data-ttu-id="0edd5-192">**Facultatif —** chaîne</span><span class="sxs-lookup"><span data-stu-id="0edd5-192">**Optional** — string</span></span>

<span data-ttu-id="0edd5-193">Identificateur unique de l’application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="0edd5-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="0edd5-194">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="0edd5-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="0edd5-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="0edd5-195">localizationInfo</span></span>

<span data-ttu-id="0edd5-196">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-196">**Optional** — object</span></span>

<span data-ttu-id="0edd5-197">Autorise la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0edd5-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="0edd5-198">Voir [localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="0edd5-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="0edd5-199">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-199">Name</span></span>| <span data-ttu-id="0edd5-200">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-200">Maximum size</span></span> | <span data-ttu-id="0edd5-201">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-201">Required</span></span> | <span data-ttu-id="0edd5-202">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="0edd5-203">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-203">✔</span></span>|<span data-ttu-id="0edd5-204">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="0edd5-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="0edd5-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="0edd5-206">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0edd5-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="0edd5-207">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-207">Name</span></span>| <span data-ttu-id="0edd5-208">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-208">Maximum size</span></span> | <span data-ttu-id="0edd5-209">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-209">Required</span></span> | <span data-ttu-id="0edd5-210">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="0edd5-211">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-211">✔</span></span>|<span data-ttu-id="0edd5-212">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="0edd5-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="0edd5-213">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-213">✔</span></span>|<span data-ttu-id="0edd5-214">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="0edd5-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="0edd5-215">icons</span><span class="sxs-lookup"><span data-stu-id="0edd5-215">icons</span></span>

<span data-ttu-id="0edd5-216">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-216">**Required** — object</span></span>

<span data-ttu-id="0edd5-217">Icônes utilisées dans l’Teams app.</span><span class="sxs-lookup"><span data-stu-id="0edd5-217">Icons used within the Teams app.</span></span> <span data-ttu-id="0edd5-218">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="0edd5-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="0edd5-219">Pour plus [d’informations,](../../concepts/build-and-test/apps-package.md#app-icons) voir Icônes.</span><span class="sxs-lookup"><span data-stu-id="0edd5-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="0edd5-220">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-220">Name</span></span>| <span data-ttu-id="0edd5-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-221">Maximum size</span></span> | <span data-ttu-id="0edd5-222">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-222">Required</span></span> | <span data-ttu-id="0edd5-223">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="0edd5-224">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="0edd5-224">32 x 32 pixels</span></span>|<span data-ttu-id="0edd5-225">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-225">✔</span></span>|<span data-ttu-id="0edd5-226">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="0edd5-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="0edd5-227">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="0edd5-227">192 x 192 pixels</span></span>|<span data-ttu-id="0edd5-228">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-228">✔</span></span>|<span data-ttu-id="0edd5-229">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="0edd5-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="0edd5-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="0edd5-230">accentColor</span></span>

<span data-ttu-id="0edd5-231">**Facultatif** — Code de couleur HTML Hex</span><span class="sxs-lookup"><span data-stu-id="0edd5-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="0edd5-232">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="0edd5-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="0edd5-233">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="0edd5-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="0edd5-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="0edd5-234">configurableTabs</span></span>

<span data-ttu-id="0edd5-235">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-235">**Optional** — array</span></span>

<span data-ttu-id="0edd5-236">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="0edd5-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="0edd5-237">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams et vous pouvez configurer les mêmes onglets plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="0edd5-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="0edd5-238">Toutefois, vous ne pouvez la définir dans le manifeste qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="0edd5-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="0edd5-239">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-239">Name</span></span>| <span data-ttu-id="0edd5-240">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-240">Type</span></span>| <span data-ttu-id="0edd5-241">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-241">Maximum size</span></span> | <span data-ttu-id="0edd5-242">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-242">Required</span></span> | <span data-ttu-id="0edd5-243">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0edd5-244">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-244">string</span></span>|<span data-ttu-id="0edd5-245">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-245">2048 characters</span></span>|<span data-ttu-id="0edd5-246">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-246">✔</span></span>|<span data-ttu-id="0edd5-247">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0edd5-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="0edd5-248">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-248">array of enums</span></span>|<span data-ttu-id="0edd5-249">1</span><span class="sxs-lookup"><span data-stu-id="0edd5-249">1</span></span>|<span data-ttu-id="0edd5-250">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-250">✔</span></span>|<span data-ttu-id="0edd5-251">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="0edd5-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="0edd5-252">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-252">boolean</span></span>|||<span data-ttu-id="0edd5-253">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="0edd5-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="0edd5-254">Valeur par défaut **: true**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="0edd5-255">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-255">array of enums</span></span>|<span data-ttu-id="0edd5-256">6 </span><span class="sxs-lookup"><span data-stu-id="0edd5-256">6</span></span>||<span data-ttu-id="0edd5-257">Ensemble `contextItem` d’étendues où un [onglet est pris en charge.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="0edd5-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="0edd5-258">Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="0edd5-259">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-259">string</span></span>|<span data-ttu-id="0edd5-260">2048</span><span class="sxs-lookup"><span data-stu-id="0edd5-260">2048</span></span>||<span data-ttu-id="0edd5-261">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0edd5-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="0edd5-262">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="0edd5-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="0edd5-263">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-263">array of enums</span></span>|<span data-ttu-id="0edd5-264">1</span><span class="sxs-lookup"><span data-stu-id="0edd5-264">1</span></span>||<span data-ttu-id="0edd5-265">Définit la façon dont votre onglet est mis à disposition dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0edd5-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="0edd5-266">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="0edd5-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="0edd5-267">staticTabs</span><span class="sxs-lookup"><span data-stu-id="0edd5-267">staticTabs</span></span>

<span data-ttu-id="0edd5-268">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-268">**Optional** — array</span></span>

<span data-ttu-id="0edd5-269">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="0edd5-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="0edd5-270">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="0edd5-271">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0edd5-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="0edd5-272">Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="0edd5-273">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="0edd5-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="0edd5-274">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-274">Name</span></span>| <span data-ttu-id="0edd5-275">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-275">Type</span></span>| <span data-ttu-id="0edd5-276">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-276">Maximum size</span></span> | <span data-ttu-id="0edd5-277">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-277">Required</span></span> | <span data-ttu-id="0edd5-278">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="0edd5-279">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-279">string</span></span>|<span data-ttu-id="0edd5-280">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-280">64 characters</span></span>|<span data-ttu-id="0edd5-281">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-281">✔</span></span>|<span data-ttu-id="0edd5-282">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="0edd5-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="0edd5-283">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-283">string</span></span>|<span data-ttu-id="0edd5-284">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-284">128 characters</span></span>|<span data-ttu-id="0edd5-285">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-285">✔</span></span>|<span data-ttu-id="0edd5-286">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="0edd5-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="0edd5-287">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-287">string</span></span>||<span data-ttu-id="0edd5-288">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-288">✔</span></span>|<span data-ttu-id="0edd5-289">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone Teams dessin.</span><span class="sxs-lookup"><span data-stu-id="0edd5-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="0edd5-290">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-290">string</span></span>|||<span data-ttu-id="0edd5-291">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="0edd5-292">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-292">string</span></span>|||<span data-ttu-id="0edd5-293">L https:// URL pointant vers les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="0edd5-294">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-294">array of enums</span></span>|<span data-ttu-id="0edd5-295">1</span><span class="sxs-lookup"><span data-stu-id="0edd5-295">1</span></span>|<span data-ttu-id="0edd5-296">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-296">✔</span></span>|<span data-ttu-id="0edd5-297">Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="0edd5-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="0edd5-298">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-298">array of enums</span></span>| <span data-ttu-id="0edd5-299">2</span><span class="sxs-lookup"><span data-stu-id="0edd5-299">2</span></span>|| <span data-ttu-id="0edd5-300">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0edd5-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="0edd5-301">La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.</span><span class="sxs-lookup"><span data-stu-id="0edd5-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="0edd5-302">Si vos onglets nécessitent des informations contextielles pour afficher  du contenu pertinent ou pour lancer un flux d’authentification, voir Obtenir le contexte de [votre onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="0edd5-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="0edd5-303">bots</span><span class="sxs-lookup"><span data-stu-id="0edd5-303">bots</span></span>

<span data-ttu-id="0edd5-304">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-304">**Optional** — array</span></span>

<span data-ttu-id="0edd5-305">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="0edd5-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="0edd5-306">L’élément est un tableau (maximum de 1 élément actuellement un seul bot est autorisé par application) avec tous les éléments &mdash; du type `object` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="0edd5-307">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="0edd5-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="0edd5-308">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-308">Name</span></span>| <span data-ttu-id="0edd5-309">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-309">Type</span></span>| <span data-ttu-id="0edd5-310">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-310">Maximum size</span></span> | <span data-ttu-id="0edd5-311">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-311">Required</span></span> | <span data-ttu-id="0edd5-312">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0edd5-313">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-313">string</span></span>|<span data-ttu-id="0edd5-314">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-314">64 characters</span></span>|<span data-ttu-id="0edd5-315">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-315">✔</span></span>|<span data-ttu-id="0edd5-316">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0edd5-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="0edd5-317">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="0edd5-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="0edd5-318">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-318">array of enums</span></span>|<span data-ttu-id="0edd5-319">3</span><span class="sxs-lookup"><span data-stu-id="0edd5-319">3</span></span>|<span data-ttu-id="0edd5-320">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-320">✔</span></span>|<span data-ttu-id="0edd5-321">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="0edd5-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0edd5-322">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="0edd5-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="0edd5-323">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-323">boolean</span></span>|||<span data-ttu-id="0edd5-324">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="0edd5-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="0edd5-325">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="0edd5-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="0edd5-326">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-326">boolean</span></span>|||<span data-ttu-id="0edd5-327">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="0edd5-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="0edd5-328">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="0edd5-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="0edd5-329">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-329">boolean</span></span>|||<span data-ttu-id="0edd5-330">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="0edd5-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="0edd5-331">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="0edd5-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="0edd5-332">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-332">boolean</span></span>|||<span data-ttu-id="0edd5-333">Valeur indiquant où un bot prend en charge les appels audio.</span><span class="sxs-lookup"><span data-stu-id="0edd5-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="0edd5-334">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="0edd5-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="0edd5-335">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="0edd5-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="0edd5-336">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="0edd5-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="0edd5-337">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="0edd5-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="0edd5-338">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-338">boolean</span></span>|||<span data-ttu-id="0edd5-339">Valeur indiquant où un bot prend en charge les appels vidéo.</span><span class="sxs-lookup"><span data-stu-id="0edd5-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="0edd5-340">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="0edd5-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="0edd5-341">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="0edd5-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="0edd5-342">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="0edd5-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="0edd5-343">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="0edd5-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="0edd5-344">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="0edd5-344">bots.commandLists</span></span>

<span data-ttu-id="0edd5-345">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0edd5-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="0edd5-346">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="0edd5-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="0edd5-347">Pour plus [d’informations,](~/bots/how-to/create-a-bot-commands-menu.md) voir les menus du bot.</span><span class="sxs-lookup"><span data-stu-id="0edd5-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="0edd5-348">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-348">Name</span></span>| <span data-ttu-id="0edd5-349">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-349">Type</span></span>| <span data-ttu-id="0edd5-350">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-350">Maximum size</span></span> | <span data-ttu-id="0edd5-351">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-351">Required</span></span> | <span data-ttu-id="0edd5-352">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="0edd5-353">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-353">array of enums</span></span>|<span data-ttu-id="0edd5-354">3</span><span class="sxs-lookup"><span data-stu-id="0edd5-354">3</span></span>|<span data-ttu-id="0edd5-355">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-355">✔</span></span>|<span data-ttu-id="0edd5-356">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="0edd5-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="0edd5-357">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="0edd5-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="0edd5-358">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-358">array of objects</span></span>|<span data-ttu-id="0edd5-359">10 </span><span class="sxs-lookup"><span data-stu-id="0edd5-359">10</span></span>|<span data-ttu-id="0edd5-360">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-360">✔</span></span>|<span data-ttu-id="0edd5-361">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="0edd5-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="0edd5-362">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="0edd5-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="0edd5-363">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="0edd5-363">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="0edd5-364">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="0edd5-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="0edd5-365">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-365">Name</span></span>| <span data-ttu-id="0edd5-366">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-366">Type</span></span>| <span data-ttu-id="0edd5-367">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-367">Maximum size</span></span> | <span data-ttu-id="0edd5-368">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-368">Required</span></span> | <span data-ttu-id="0edd5-369">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="0edd5-370">title</span><span class="sxs-lookup"><span data-stu-id="0edd5-370">title</span></span>|<span data-ttu-id="0edd5-371">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-371">string</span></span>|<span data-ttu-id="0edd5-372">12 </span><span class="sxs-lookup"><span data-stu-id="0edd5-372">12</span></span>|<span data-ttu-id="0edd5-373">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-373">✔</span></span>|<span data-ttu-id="0edd5-374">Nom de la commande du bot</span><span class="sxs-lookup"><span data-stu-id="0edd5-374">The bot command name</span></span>|
|<span data-ttu-id="0edd5-375">description</span><span class="sxs-lookup"><span data-stu-id="0edd5-375">description</span></span>|<span data-ttu-id="0edd5-376">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-376">string</span></span>|<span data-ttu-id="0edd5-377">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-377">128 characters</span></span>|<span data-ttu-id="0edd5-378">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-378">✔</span></span>|<span data-ttu-id="0edd5-379">Description de texte simple ou exemple de syntaxe de commande et de ses arguments.</span><span class="sxs-lookup"><span data-stu-id="0edd5-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="0edd5-380">connecteurs</span><span class="sxs-lookup"><span data-stu-id="0edd5-380">connectors</span></span>

<span data-ttu-id="0edd5-381">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-381">**Optional** — array</span></span>

<span data-ttu-id="0edd5-382">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="0edd5-383">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0edd5-384">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="0edd5-385">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-385">Name</span></span>| <span data-ttu-id="0edd5-386">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-386">Type</span></span>| <span data-ttu-id="0edd5-387">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-387">Maximum size</span></span> | <span data-ttu-id="0edd5-388">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-388">Required</span></span> | <span data-ttu-id="0edd5-389">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0edd5-390">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-390">string</span></span>|<span data-ttu-id="0edd5-391">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-391">2048 characters</span></span>|<span data-ttu-id="0edd5-392">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-392">✔</span></span>|<span data-ttu-id="0edd5-393">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="0edd5-394">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="0edd5-394">array of enums</span></span>|<span data-ttu-id="0edd5-395">1</span><span class="sxs-lookup"><span data-stu-id="0edd5-395">1</span></span>|<span data-ttu-id="0edd5-396">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-396">✔</span></span>|<span data-ttu-id="0edd5-397">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="0edd5-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0edd5-398">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="0edd5-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="0edd5-399">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-399">string</span></span>|<span data-ttu-id="0edd5-400">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-400">64 characters</span></span>|<span data-ttu-id="0edd5-401">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-401">✔</span></span>|<span data-ttu-id="0edd5-402">Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="0edd5-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="0edd5-403">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="0edd5-403">composeExtensions</span></span>

<span data-ttu-id="0edd5-404">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-404">**Optional** — array</span></span>

<span data-ttu-id="0edd5-405">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="0edd5-406">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="0edd5-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="0edd5-407">L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0edd5-408">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0edd5-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="0edd5-409">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-409">Name</span></span>| <span data-ttu-id="0edd5-410">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-410">Type</span></span> | <span data-ttu-id="0edd5-411">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-411">Maximum Size</span></span> | <span data-ttu-id="0edd5-412">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="0edd5-412">Required</span></span> | <span data-ttu-id="0edd5-413">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0edd5-414">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-414">string</span></span>|<span data-ttu-id="0edd5-415">64</span><span class="sxs-lookup"><span data-stu-id="0edd5-415">64</span></span>|<span data-ttu-id="0edd5-416">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-416">✔</span></span>|<span data-ttu-id="0edd5-417">ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0edd5-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="0edd5-418">Cela peut être identique à l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="0edd5-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="0edd5-419">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-419">array of objects</span></span>|<span data-ttu-id="0edd5-420">10 </span><span class="sxs-lookup"><span data-stu-id="0edd5-420">10</span></span>|<span data-ttu-id="0edd5-421">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-421">✔</span></span>|<span data-ttu-id="0edd5-422">Tableau de commandes pris en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="0edd5-422">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0edd5-423">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-423">boolean</span></span>|||<span data-ttu-id="0edd5-424">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="0edd5-425">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="0edd5-426">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-426">array of Objects</span></span>|<span data-ttu-id="0edd5-427">5 </span><span class="sxs-lookup"><span data-stu-id="0edd5-427">5</span></span>||<span data-ttu-id="0edd5-428">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="0edd5-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="0edd5-429">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-429">string</span></span>|||<span data-ttu-id="0edd5-430">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="0edd5-430">The type of message handler.</span></span> <span data-ttu-id="0edd5-431">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="0edd5-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="0edd5-432">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="0edd5-432">array of Strings</span></span>|||<span data-ttu-id="0edd5-433">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="0edd5-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="0edd5-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="0edd5-434">composeExtensions.commands</span></span>

<span data-ttu-id="0edd5-435">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="0edd5-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="0edd5-436">Chaque commande s’affiche Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="0edd5-437">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="0edd5-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="0edd5-438">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="0edd5-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="0edd5-439">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-439">Name</span></span>| <span data-ttu-id="0edd5-440">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-440">Type</span></span>| <span data-ttu-id="0edd5-441">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-441">Maximum size</span></span> | <span data-ttu-id="0edd5-442">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-442">Required</span></span> | <span data-ttu-id="0edd5-443">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0edd5-444">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-444">string</span></span>|<span data-ttu-id="0edd5-445">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-445">64 characters</span></span>|<span data-ttu-id="0edd5-446">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-446">✔</span></span>|<span data-ttu-id="0edd5-447">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="0edd5-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="0edd5-448">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-448">string</span></span>|<span data-ttu-id="0edd5-449">32 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-449">32 characters</span></span>|<span data-ttu-id="0edd5-450">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-450">✔</span></span>|<span data-ttu-id="0edd5-451">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="0edd5-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="0edd5-452">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-452">string</span></span>|<span data-ttu-id="0edd5-453">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-453">64 characters</span></span>||<span data-ttu-id="0edd5-454">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="0edd5-454">Type of the command.</span></span> <span data-ttu-id="0edd5-455">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="0edd5-455">One of `query` or `action`.</span></span> <span data-ttu-id="0edd5-456">Par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="0edd5-457">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-457">string</span></span>|<span data-ttu-id="0edd5-458">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-458">128 characters</span></span>||<span data-ttu-id="0edd5-459">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="0edd5-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="0edd5-460">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-460">boolean</span></span>|||<span data-ttu-id="0edd5-461">Une valeur booléle indique si la commande s’exécute initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="0edd5-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="0edd5-462">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="0edd5-463">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="0edd5-463">array of Strings</span></span>|<span data-ttu-id="0edd5-464">3</span><span class="sxs-lookup"><span data-stu-id="0edd5-464">3</span></span>||<span data-ttu-id="0edd5-465">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="0edd5-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="0edd5-466">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="0edd5-467">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="0edd5-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="0edd5-468">booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-468">boolean</span></span>|||<span data-ttu-id="0edd5-469">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="0edd5-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="0edd5-470">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="0edd5-471">objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-471">object</span></span>|||<span data-ttu-id="0edd5-472">Spécifiez le module de tâche à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0edd5-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="0edd5-473">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-473">string</span></span>|<span data-ttu-id="0edd5-474">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-474">64 characters</span></span>||<span data-ttu-id="0edd5-475">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="0edd5-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="0edd5-476">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-476">string</span></span>|||<span data-ttu-id="0edd5-477">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="0edd5-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="0edd5-478">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-478">string</span></span>|||<span data-ttu-id="0edd5-479">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="0edd5-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="0edd5-480">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-480">string</span></span>|||<span data-ttu-id="0edd5-481">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="0edd5-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="0edd5-482">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-482">array of object</span></span>|<span data-ttu-id="0edd5-483">5 éléments</span><span class="sxs-lookup"><span data-stu-id="0edd5-483">5 items</span></span>|<span data-ttu-id="0edd5-484">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-484">✔</span></span>|<span data-ttu-id="0edd5-485">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="0edd5-485">The list of parameters the command takes.</span></span> <span data-ttu-id="0edd5-486">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="0edd5-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="0edd5-487">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-487">string</span></span>|<span data-ttu-id="0edd5-488">64 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-488">64 characters</span></span>|<span data-ttu-id="0edd5-489">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-489">✔</span></span>|<span data-ttu-id="0edd5-490">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="0edd5-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="0edd5-491">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="0edd5-492">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-492">string</span></span>|<span data-ttu-id="0edd5-493">32 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-493">32 characters</span></span>|<span data-ttu-id="0edd5-494">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-494">✔</span></span>|<span data-ttu-id="0edd5-495">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="0edd5-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="0edd5-496">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-496">string</span></span>|<span data-ttu-id="0edd5-497">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-497">128 characters</span></span>||<span data-ttu-id="0edd5-498">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="0edd5-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="0edd5-499">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-499">string</span></span>|<span data-ttu-id="0edd5-500">512 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-500">512 characters</span></span>||<span data-ttu-id="0edd5-501">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="0edd5-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="0edd5-502">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-502">string</span></span>|<span data-ttu-id="0edd5-503">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-503">128 characters</span></span>||<span data-ttu-id="0edd5-504">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="0edd5-505">L’une `text, textarea, number, date, time, toggle, choiceset` des .</span><span class="sxs-lookup"><span data-stu-id="0edd5-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="0edd5-506">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-506">array of objects</span></span>|<span data-ttu-id="0edd5-507">10 éléments</span><span class="sxs-lookup"><span data-stu-id="0edd5-507">10 items</span></span>||<span data-ttu-id="0edd5-508">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="0edd5-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="0edd5-509">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="0edd5-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="0edd5-510">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-510">string</span></span>|<span data-ttu-id="0edd5-511">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-511">128 characters</span></span>|<span data-ttu-id="0edd5-512">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-512">✔</span></span>|<span data-ttu-id="0edd5-513">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="0edd5-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="0edd5-514">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-514">string</span></span>|<span data-ttu-id="0edd5-515">512 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-515">512 characters</span></span>|<span data-ttu-id="0edd5-516">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-516">✔</span></span>|<span data-ttu-id="0edd5-517">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="0edd5-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="0edd5-518">autorisations</span><span class="sxs-lookup"><span data-stu-id="0edd5-518">permissions</span></span>

<span data-ttu-id="0edd5-519">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="0edd5-519">**Optional** — array of strings</span></span>

<span data-ttu-id="0edd5-520">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` fonctionne l’extension.</span><span class="sxs-lookup"><span data-stu-id="0edd5-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="0edd5-521">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="0edd5-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="0edd5-522">`identity`&emsp;Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="0edd5-522">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="0edd5-523">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="0edd5-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="0edd5-524">Si vous modifiez ces autorisations pendant la mise à jour de l’application, vos utilisateurs répètent le processus de consentement après avoir exécuté l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="0edd5-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="0edd5-525">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) Mise à jour de votre application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="0edd5-526">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="0edd5-526">devicePermissions</span></span>

<span data-ttu-id="0edd5-527">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="0edd5-527">**Optional** — array of strings</span></span>

<span data-ttu-id="0edd5-528">Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès.</span><span class="sxs-lookup"><span data-stu-id="0edd5-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="0edd5-529">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="0edd5-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="0edd5-530">validDomains</span><span class="sxs-lookup"><span data-stu-id="0edd5-530">validDomains</span></span>

<span data-ttu-id="0edd5-531">**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué</span><span class="sxs-lookup"><span data-stu-id="0edd5-531">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="0edd5-532">Liste des domaines valides pour les sites web que l’application s’attend à charger dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="0edd5-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="0edd5-533">Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="0edd5-534">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="0edd5-535">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="0edd5-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="0edd5-536">Il **n’est** pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="0edd5-537">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="0edd5-538">Teams applications qui nécessitent leurs propres URL sharepoint pour fonctionner bien, inclut « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="0edd5-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0edd5-539">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="0edd5-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="0edd5-540">Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0edd5-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="0edd5-541">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="0edd5-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="0edd5-542">webApplicationInfo</span></span>

<span data-ttu-id="0edd5-543">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-543">**Optional** — object</span></span>

<span data-ttu-id="0edd5-544">Fournissez votre ID d’Azure Active Directory (AAD) et des informations microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="0edd5-545">Si votre application est inscrite dans AAD, vous devez fournir l’ID de l’application, afin que les administrateurs peuvent facilement passer en revue les autorisations et accorder leur consentement dans Teams centre d’administration.</span><span class="sxs-lookup"><span data-stu-id="0edd5-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="0edd5-546">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-546">Name</span></span>| <span data-ttu-id="0edd5-547">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-547">Type</span></span>| <span data-ttu-id="0edd5-548">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-548">Maximum size</span></span> | <span data-ttu-id="0edd5-549">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-549">Required</span></span> | <span data-ttu-id="0edd5-550">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0edd5-551">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-551">string</span></span>|<span data-ttu-id="0edd5-552">36 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-552">36 characters</span></span>|<span data-ttu-id="0edd5-553">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-553">✔</span></span>|<span data-ttu-id="0edd5-554">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-554">AAD application id of the app.</span></span> <span data-ttu-id="0edd5-555">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="0edd5-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="0edd5-556">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-556">string</span></span>|<span data-ttu-id="0edd5-557">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-557">2048 characters</span></span>|<span data-ttu-id="0edd5-558">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-558">✔</span></span>|<span data-ttu-id="0edd5-559">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="0edd5-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="0edd5-560">**REMARQUE :** Si vous n’utilisez pas l’oD SSO, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, pour éviter une réponse https://notapplicable d’erreur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="0edd5-561">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="0edd5-561">array of strings</span></span>|<span data-ttu-id="0edd5-562">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-562">128 characters</span></span>||<span data-ttu-id="0edd5-563">Spécifiez le consentement précis [spécifique à une ressource.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="0edd5-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="0edd5-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="0edd5-564">showLoadingIndicator</span></span>

<span data-ttu-id="0edd5-565">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-565">**Optional** — boolean</span></span>

<span data-ttu-id="0edd5-566">Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="0edd5-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="0edd5-567">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="0edd5-568">Si vous sélectionnez true dans le manifeste de votre application, pour charger la page correctement, modifiez les pages de contenu de vos onglets et modules de tâche comme décrit dans Afficher un document d’indicateur de chargement `showLoadingIndicator` natif. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="0edd5-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="0edd5-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="0edd5-569">isFullScreen</span></span>

 <span data-ttu-id="0edd5-570">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="0edd5-570">**Optional** — boolean</span></span>

<span data-ttu-id="0edd5-571">Indiquez l’endroit où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="0edd5-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="0edd5-572">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="0edd5-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="0edd5-573">activités</span><span class="sxs-lookup"><span data-stu-id="0edd5-573">activities</span></span>

<span data-ttu-id="0edd5-574">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-574">**Optional** — object</span></span>

<span data-ttu-id="0edd5-575">Définissez les propriétés que votre application utilise pour publier un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="0edd5-576">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-576">Name</span></span>| <span data-ttu-id="0edd5-577">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-577">Type</span></span>| <span data-ttu-id="0edd5-578">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-578">Maximum size</span></span> | <span data-ttu-id="0edd5-579">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-579">Required</span></span> | <span data-ttu-id="0edd5-580">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="0edd5-581">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="0edd5-581">array of Objects</span></span>|<span data-ttu-id="0edd5-582">128 éléments</span><span class="sxs-lookup"><span data-stu-id="0edd5-582">128 items</span></span>| | <span data-ttu-id="0edd5-583">Fournissez les types d’activités que votre application peut publier dans un flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0edd5-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="0edd5-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="0edd5-584">activities.activityTypes</span></span>

|<span data-ttu-id="0edd5-585">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-585">Name</span></span>| <span data-ttu-id="0edd5-586">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-586">Type</span></span>| <span data-ttu-id="0edd5-587">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-587">Maximum size</span></span> | <span data-ttu-id="0edd5-588">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-588">Required</span></span> | <span data-ttu-id="0edd5-589">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="0edd5-590">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-590">string</span></span>|<span data-ttu-id="0edd5-591">32 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-591">32 characters</span></span>|<span data-ttu-id="0edd5-592">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-592">✔</span></span>|<span data-ttu-id="0edd5-593">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="0edd5-593">The notification type.</span></span> <span data-ttu-id="0edd5-594">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="0edd5-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="0edd5-595">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-595">string</span></span>|<span data-ttu-id="0edd5-596">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-596">128 characters</span></span>|<span data-ttu-id="0edd5-597">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-597">✔</span></span>|<span data-ttu-id="0edd5-598">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="0edd5-598">A brief description of the notification.</span></span> <span data-ttu-id="0edd5-599">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="0edd5-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="0edd5-600">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-600">string</span></span>|<span data-ttu-id="0edd5-601">128 caractères</span><span class="sxs-lookup"><span data-stu-id="0edd5-601">128 characters</span></span>|<span data-ttu-id="0edd5-602">✔</span><span class="sxs-lookup"><span data-stu-id="0edd5-602">✔</span></span>|<span data-ttu-id="0edd5-603">Ex: « {actor} created task {taskId} for you »</span><span class="sxs-lookup"><span data-stu-id="0edd5-603">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="0edd5-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="0edd5-604">defaultInstallScope</span></span>

<span data-ttu-id="0edd5-605">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="0edd5-605">**Optional** - string</span></span>

<span data-ttu-id="0edd5-606">Spécifie l’étendue d’installation définie par défaut pour cette application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="0edd5-607">L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="0edd5-608">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="0edd5-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="0edd5-609">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="0edd5-609">defaultGroupCapability</span></span>

<span data-ttu-id="0edd5-610">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="0edd5-610">**Optional** - object</span></span>

<span data-ttu-id="0edd5-611">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="0edd5-612">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="0edd5-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="0edd5-613">Nom</span><span class="sxs-lookup"><span data-stu-id="0edd5-613">Name</span></span>| <span data-ttu-id="0edd5-614">Type</span><span class="sxs-lookup"><span data-stu-id="0edd5-614">Type</span></span>| <span data-ttu-id="0edd5-615">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="0edd5-615">Maximum size</span></span> | <span data-ttu-id="0edd5-616">Requis</span><span class="sxs-lookup"><span data-stu-id="0edd5-616">Required</span></span> | <span data-ttu-id="0edd5-617">Description</span><span class="sxs-lookup"><span data-stu-id="0edd5-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="0edd5-618">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-618">string</span></span>|||<span data-ttu-id="0edd5-619">Lorsque l’étendue d’installation sélectionnée `team` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="0edd5-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="0edd5-620">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="0edd5-621">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-621">string</span></span>|||<span data-ttu-id="0edd5-622">Lorsque l’étendue d’installation sélectionnée `groupchat` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="0edd5-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="0edd5-623">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="0edd5-624">string</span><span class="sxs-lookup"><span data-stu-id="0edd5-624">string</span></span>|||<span data-ttu-id="0edd5-625">Lorsque l’étendue d’installation sélectionnée `meetings` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="0edd5-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="0edd5-626">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="0edd5-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="0edd5-627">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="0edd5-627">configurableProperties</span></span>

<span data-ttu-id="0edd5-628">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="0edd5-628">**Optional** - array</span></span>

<span data-ttu-id="0edd5-629">Le `configurableProperties` bloc définit les propriétés d’application que Teams administrateur peut personnaliser.</span><span class="sxs-lookup"><span data-stu-id="0edd5-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="0edd5-630">Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="0edd5-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="0edd5-631">Au moins une propriété doit être définie.</span><span class="sxs-lookup"><span data-stu-id="0edd5-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="0edd5-632">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="0edd5-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="0edd5-633">En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="0edd5-634">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0edd5-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="0edd5-635">`name`: permet à l’administrateur de modifier le nom complet de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="0edd5-636">`shortDescription`: permet à l’administrateur de modifier la description courte de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="0edd5-637">`longDescription`: permet à l’administrateur de modifier la description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="0edd5-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="0edd5-638">`smallImageUrl`: il s’agit `outline` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="0edd5-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="0edd5-639">`largeImageUrl`: il s’agit `color` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="0edd5-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="0edd5-640">`accentColor`: il s’agit de la couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="0edd5-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="0edd5-641">`websiteUrl`: il s’agit https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="0edd5-642">`privacyUrl`: il s’agit https:// URL de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="0edd5-643">`termsOfUseUrl`: il s’agit https:// URL des conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="0edd5-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


