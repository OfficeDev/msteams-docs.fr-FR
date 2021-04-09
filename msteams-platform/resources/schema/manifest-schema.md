---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
keywords: schéma de manifeste teams
ms.openlocfilehash: 8c77d2e82c65a11b67eb6a223313f477238517d9
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634522"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="32585-104">Référence : schéma de manifeste pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="32585-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="32585-105">Le manifeste Teams décrit comment l’application s’intègre au produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="32585-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="32585-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="32585-107">Les versions précédentes 1.0-1.4 sont également pris en charge (à l’aide de « v1.x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="32585-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="32585-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="32585-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="32585-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="32585-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
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
  }
}
```

<span data-ttu-id="32585-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="32585-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="32585-111">$schema</span><span class="sxs-lookup"><span data-stu-id="32585-111">$schema</span></span>

<span data-ttu-id="32585-112">Chaîne facultative, mais recommandée</span><span class="sxs-lookup"><span data-stu-id="32585-112">Optional, but recommended — string</span></span>

<span data-ttu-id="32585-113">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="32585-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="32585-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="32585-114">manifestVersion</span></span>

<span data-ttu-id="32585-115">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="32585-115">**Required** — string</span></span>

<span data-ttu-id="32585-116">Version du schéma de manifeste que ce manifeste utilise.</span><span class="sxs-lookup"><span data-stu-id="32585-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="32585-117">Elle doit être 1,9.</span><span class="sxs-lookup"><span data-stu-id="32585-117">It must be 1.9.</span></span>

## <a name="version"></a><span data-ttu-id="32585-118">version</span><span class="sxs-lookup"><span data-stu-id="32585-118">version</span></span>

<span data-ttu-id="32585-119">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="32585-119">**Required** — string</span></span>

<span data-ttu-id="32585-120">Version d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="32585-120">The version of a specific app.</span></span> <span data-ttu-id="32585-121">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="32585-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="32585-122">De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="32585-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="32585-123">Si cette application a été soumise au Store, le nouveau manifeste doit être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="32585-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="32585-124">Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.</span><span class="sxs-lookup"><span data-stu-id="32585-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="32585-125">Si l’application demande des autorisations change, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="32585-126">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="32585-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="32585-127">id</span><span class="sxs-lookup"><span data-stu-id="32585-127">id</span></span>

<span data-ttu-id="32585-128">**Obligatoire** — ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="32585-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="32585-129">L’ID est un identificateur unique généré par Microsoft pour l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="32585-130">Vous avez un ID si votre bot est inscrit via Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32585-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="32585-131">Vous devez entrer l’ID ici.</span><span class="sxs-lookup"><span data-stu-id="32585-131">You must enter the ID here.</span></span> <span data-ttu-id="32585-132">Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft ([Mes applications).](https://apps.dev.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="32585-132">Otherwise, you must generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)).</span></span> <span data-ttu-id="32585-133">Utilisez le même ID si vous ajoutez un bot.</span><span class="sxs-lookup"><span data-stu-id="32585-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="32585-134">Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="32585-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="32585-135">developer</span><span class="sxs-lookup"><span data-stu-id="32585-135">developer</span></span>

<span data-ttu-id="32585-136">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-136">**Required** — object</span></span>

<span data-ttu-id="32585-137">Fournit des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="32585-137">Gives information about your company.</span></span> <span data-ttu-id="32585-138">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="32585-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="32585-139">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) les instructions de publication.</span><span class="sxs-lookup"><span data-stu-id="32585-139">See the [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="32585-140">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-140">Name</span></span>| <span data-ttu-id="32585-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-141">Maximum size</span></span> | <span data-ttu-id="32585-142">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-142">Required</span></span> | <span data-ttu-id="32585-143">Description</span><span class="sxs-lookup"><span data-stu-id="32585-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="32585-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-144">32 characters</span></span>|<span data-ttu-id="32585-145">✔</span><span class="sxs-lookup"><span data-stu-id="32585-145">✔</span></span>|<span data-ttu-id="32585-146">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="32585-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="32585-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-147">2048 characters</span></span>|<span data-ttu-id="32585-148">✔</span><span class="sxs-lookup"><span data-stu-id="32585-148">✔</span></span>|<span data-ttu-id="32585-149">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="32585-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="32585-150">Ce lien doit prendre les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="32585-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="32585-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-151">2048 characters</span></span>|<span data-ttu-id="32585-152">✔</span><span class="sxs-lookup"><span data-stu-id="32585-152">✔</span></span>|<span data-ttu-id="32585-153">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="32585-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="32585-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-154">2048 characters</span></span>|<span data-ttu-id="32585-155">✔</span><span class="sxs-lookup"><span data-stu-id="32585-155">✔</span></span>|<span data-ttu-id="32585-156">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="32585-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="32585-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-157">10 characters</span></span>| |<span data-ttu-id="32585-158">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="32585-159">nom</span><span class="sxs-lookup"><span data-stu-id="32585-159">name</span></span>

<span data-ttu-id="32585-160">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-160">**Required** — object</span></span>

<span data-ttu-id="32585-161">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="32585-162">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="32585-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="32585-163">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="32585-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="32585-164">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-164">Name</span></span>| <span data-ttu-id="32585-165">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-165">Maximum size</span></span> | <span data-ttu-id="32585-166">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-166">Required</span></span> | <span data-ttu-id="32585-167">Description</span><span class="sxs-lookup"><span data-stu-id="32585-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="32585-168">30 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-168">30 characters</span></span>|<span data-ttu-id="32585-169">✔</span><span class="sxs-lookup"><span data-stu-id="32585-169">✔</span></span>|<span data-ttu-id="32585-170">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="32585-171">100 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-171">100 characters</span></span>||<span data-ttu-id="32585-172">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="32585-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="32585-173">description</span><span class="sxs-lookup"><span data-stu-id="32585-173">description</span></span>

<span data-ttu-id="32585-174">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-174">**Required** — object</span></span>

<span data-ttu-id="32585-175">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="32585-175">Describes your app to users.</span></span> <span data-ttu-id="32585-176">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="32585-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="32585-177">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="32585-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="32585-178">Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="32585-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="32585-179">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="32585-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="32585-180">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="32585-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="32585-181">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-181">Name</span></span>| <span data-ttu-id="32585-182">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-182">Maximum size</span></span> | <span data-ttu-id="32585-183">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-183">Required</span></span> | <span data-ttu-id="32585-184">Description</span><span class="sxs-lookup"><span data-stu-id="32585-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="32585-185">80 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-185">80 characters</span></span>|<span data-ttu-id="32585-186">✔</span><span class="sxs-lookup"><span data-stu-id="32585-186">✔</span></span>|<span data-ttu-id="32585-187">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="32585-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="32585-188">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-188">4000 characters</span></span>|<span data-ttu-id="32585-189">✔</span><span class="sxs-lookup"><span data-stu-id="32585-189">✔</span></span>|<span data-ttu-id="32585-190">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="32585-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="32585-191">packageName</span><span class="sxs-lookup"><span data-stu-id="32585-191">packageName</span></span>

<span data-ttu-id="32585-192">**Facultatif —** chaîne</span><span class="sxs-lookup"><span data-stu-id="32585-192">**Optional** — string</span></span>

<span data-ttu-id="32585-193">Identificateur unique de l’application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="32585-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="32585-194">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="32585-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="32585-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="32585-195">localizationInfo</span></span>

<span data-ttu-id="32585-196">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-196">**Optional** — object</span></span>

<span data-ttu-id="32585-197">Autorise la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="32585-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="32585-198">Voir [localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="32585-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="32585-199">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-199">Name</span></span>| <span data-ttu-id="32585-200">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-200">Maximum size</span></span> | <span data-ttu-id="32585-201">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-201">Required</span></span> | <span data-ttu-id="32585-202">Description</span><span class="sxs-lookup"><span data-stu-id="32585-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="32585-203">✔</span><span class="sxs-lookup"><span data-stu-id="32585-203">✔</span></span>|<span data-ttu-id="32585-204">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="32585-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="32585-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="32585-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="32585-206">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="32585-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="32585-207">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-207">Name</span></span>| <span data-ttu-id="32585-208">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-208">Maximum size</span></span> | <span data-ttu-id="32585-209">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-209">Required</span></span> | <span data-ttu-id="32585-210">Description</span><span class="sxs-lookup"><span data-stu-id="32585-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="32585-211">✔</span><span class="sxs-lookup"><span data-stu-id="32585-211">✔</span></span>|<span data-ttu-id="32585-212">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="32585-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="32585-213">✔</span><span class="sxs-lookup"><span data-stu-id="32585-213">✔</span></span>|<span data-ttu-id="32585-214">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="32585-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="32585-215">icons</span><span class="sxs-lookup"><span data-stu-id="32585-215">icons</span></span>

<span data-ttu-id="32585-216">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-216">**Required** — object</span></span>

<span data-ttu-id="32585-217">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-217">Icons used within the Teams app.</span></span> <span data-ttu-id="32585-218">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="32585-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="32585-219">Pour plus [d’informations,](../../concepts/build-and-test/apps-package.md#app-icons) voir Icônes.</span><span class="sxs-lookup"><span data-stu-id="32585-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="32585-220">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-220">Name</span></span>| <span data-ttu-id="32585-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-221">Maximum size</span></span> | <span data-ttu-id="32585-222">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-222">Required</span></span> | <span data-ttu-id="32585-223">Description</span><span class="sxs-lookup"><span data-stu-id="32585-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="32585-224">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="32585-224">32 x 32 pixels</span></span>|<span data-ttu-id="32585-225">✔</span><span class="sxs-lookup"><span data-stu-id="32585-225">✔</span></span>|<span data-ttu-id="32585-226">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="32585-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="32585-227">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="32585-227">192 x 192 pixels</span></span>|<span data-ttu-id="32585-228">✔</span><span class="sxs-lookup"><span data-stu-id="32585-228">✔</span></span>|<span data-ttu-id="32585-229">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="32585-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="32585-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="32585-230">accentColor</span></span>

<span data-ttu-id="32585-231">**Facultatif** — Code de couleur HTML Hex</span><span class="sxs-lookup"><span data-stu-id="32585-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="32585-232">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="32585-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="32585-233">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="32585-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="32585-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="32585-234">configurableTabs</span></span>

<span data-ttu-id="32585-235">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="32585-235">**Optional** — array</span></span>

<span data-ttu-id="32585-236">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="32585-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="32585-237">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams (et non personnelle), et actuellement, un seul **onglet** par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-237">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="32585-238">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-238">Name</span></span>| <span data-ttu-id="32585-239">Type</span><span class="sxs-lookup"><span data-stu-id="32585-239">Type</span></span>| <span data-ttu-id="32585-240">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-240">Maximum size</span></span> | <span data-ttu-id="32585-241">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-241">Required</span></span> | <span data-ttu-id="32585-242">Description</span><span class="sxs-lookup"><span data-stu-id="32585-242">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="32585-243">string</span><span class="sxs-lookup"><span data-stu-id="32585-243">string</span></span>|<span data-ttu-id="32585-244">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-244">2048 characters</span></span>|<span data-ttu-id="32585-245">✔</span><span class="sxs-lookup"><span data-stu-id="32585-245">✔</span></span>|<span data-ttu-id="32585-246">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="32585-246">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="32585-247">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-247">array of enums</span></span>|<span data-ttu-id="32585-248">1</span><span class="sxs-lookup"><span data-stu-id="32585-248">1</span></span>|<span data-ttu-id="32585-249">✔</span><span class="sxs-lookup"><span data-stu-id="32585-249">✔</span></span>|<span data-ttu-id="32585-250">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="32585-250">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="32585-251">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-251">boolean</span></span>|||<span data-ttu-id="32585-252">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="32585-252">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="32585-253">Valeur par défaut **: true**.</span><span class="sxs-lookup"><span data-stu-id="32585-253">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="32585-254">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-254">array of enums</span></span>|<span data-ttu-id="32585-255">6 </span><span class="sxs-lookup"><span data-stu-id="32585-255">6</span></span>||<span data-ttu-id="32585-256">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-256">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="32585-257">Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="32585-257">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="32585-258">string</span><span class="sxs-lookup"><span data-stu-id="32585-258">string</span></span>|<span data-ttu-id="32585-259">2048</span><span class="sxs-lookup"><span data-stu-id="32585-259">2048</span></span>||<span data-ttu-id="32585-260">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="32585-260">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="32585-261">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="32585-261">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="32585-262">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-262">array of enums</span></span>|<span data-ttu-id="32585-263">1</span><span class="sxs-lookup"><span data-stu-id="32585-263">1</span></span>||<span data-ttu-id="32585-264">Définit la façon dont votre onglet est mis à disposition dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="32585-264">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="32585-265">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="32585-265">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="32585-266">staticTabs</span><span class="sxs-lookup"><span data-stu-id="32585-266">staticTabs</span></span>

<span data-ttu-id="32585-267">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="32585-267">**Optional** — array</span></span>

<span data-ttu-id="32585-268">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="32585-268">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="32585-269">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-269">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="32585-270">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-270">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="32585-271">Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="32585-271">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="32585-272">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="32585-272">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="32585-273">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-273">Name</span></span>| <span data-ttu-id="32585-274">Type</span><span class="sxs-lookup"><span data-stu-id="32585-274">Type</span></span>| <span data-ttu-id="32585-275">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-275">Maximum size</span></span> | <span data-ttu-id="32585-276">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-276">Required</span></span> | <span data-ttu-id="32585-277">Description</span><span class="sxs-lookup"><span data-stu-id="32585-277">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="32585-278">string</span><span class="sxs-lookup"><span data-stu-id="32585-278">string</span></span>|<span data-ttu-id="32585-279">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-279">64 characters</span></span>|<span data-ttu-id="32585-280">✔</span><span class="sxs-lookup"><span data-stu-id="32585-280">✔</span></span>|<span data-ttu-id="32585-281">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="32585-281">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="32585-282">string</span><span class="sxs-lookup"><span data-stu-id="32585-282">string</span></span>|<span data-ttu-id="32585-283">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-283">128 characters</span></span>|<span data-ttu-id="32585-284">✔</span><span class="sxs-lookup"><span data-stu-id="32585-284">✔</span></span>|<span data-ttu-id="32585-285">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="32585-285">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="32585-286">string</span><span class="sxs-lookup"><span data-stu-id="32585-286">string</span></span>||<span data-ttu-id="32585-287">✔</span><span class="sxs-lookup"><span data-stu-id="32585-287">✔</span></span>|<span data-ttu-id="32585-288">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans le canevas Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="32585-289">string</span><span class="sxs-lookup"><span data-stu-id="32585-289">string</span></span>|||<span data-ttu-id="32585-290">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="32585-290">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="32585-291">string</span><span class="sxs-lookup"><span data-stu-id="32585-291">string</span></span>|||<span data-ttu-id="32585-292">L https:// URL pointant vers les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32585-292">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="32585-293">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-293">array of enums</span></span>|<span data-ttu-id="32585-294">1</span><span class="sxs-lookup"><span data-stu-id="32585-294">1</span></span>|<span data-ttu-id="32585-295">✔</span><span class="sxs-lookup"><span data-stu-id="32585-295">✔</span></span>|<span data-ttu-id="32585-296">Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="32585-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="32585-297">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-297">array of enums</span></span>| <span data-ttu-id="32585-298">2</span><span class="sxs-lookup"><span data-stu-id="32585-298">2</span></span>|| <span data-ttu-id="32585-299">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-299">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="32585-300">Si vos onglets nécessitent des informations contextielles pour afficher  du contenu pertinent ou pour lancer un flux d’authentification, voir Obtenir le contexte de votre [onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="32585-300">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="32585-301">bots</span><span class="sxs-lookup"><span data-stu-id="32585-301">bots</span></span>

<span data-ttu-id="32585-302">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="32585-302">**Optional** — array</span></span>

<span data-ttu-id="32585-303">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="32585-303">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="32585-304">L’élément est un tableau (maximum de 1 élément actuellement un seul bot est autorisé par application) avec tous les éléments &mdash; du type `object` .</span><span class="sxs-lookup"><span data-stu-id="32585-304">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="32585-305">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="32585-305">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="32585-306">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-306">Name</span></span>| <span data-ttu-id="32585-307">Type</span><span class="sxs-lookup"><span data-stu-id="32585-307">Type</span></span>| <span data-ttu-id="32585-308">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-308">Maximum size</span></span> | <span data-ttu-id="32585-309">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-309">Required</span></span> | <span data-ttu-id="32585-310">Description</span><span class="sxs-lookup"><span data-stu-id="32585-310">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="32585-311">string</span><span class="sxs-lookup"><span data-stu-id="32585-311">string</span></span>|<span data-ttu-id="32585-312">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-312">64 characters</span></span>|<span data-ttu-id="32585-313">✔</span><span class="sxs-lookup"><span data-stu-id="32585-313">✔</span></span>|<span data-ttu-id="32585-314">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="32585-314">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="32585-315">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="32585-315">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="32585-316">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-316">array of enums</span></span>|<span data-ttu-id="32585-317">3</span><span class="sxs-lookup"><span data-stu-id="32585-317">3</span></span>|<span data-ttu-id="32585-318">✔</span><span class="sxs-lookup"><span data-stu-id="32585-318">✔</span></span>|<span data-ttu-id="32585-319">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="32585-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="32585-320">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="32585-320">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="32585-321">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-321">boolean</span></span>|||<span data-ttu-id="32585-322">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="32585-322">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="32585-323">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="32585-323">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="32585-324">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-324">boolean</span></span>|||<span data-ttu-id="32585-325">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="32585-325">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="32585-326">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="32585-326">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="32585-327">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-327">boolean</span></span>|||<span data-ttu-id="32585-328">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="32585-328">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="32585-329">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="32585-329">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="32585-330">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-330">boolean</span></span>|||<span data-ttu-id="32585-331">Valeur indiquant où un bot prend en charge les appels audio.</span><span class="sxs-lookup"><span data-stu-id="32585-331">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="32585-332">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="32585-332">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="32585-333">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="32585-333">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="32585-334">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="32585-334">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="32585-335">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="32585-335">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="32585-336">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-336">boolean</span></span>|||<span data-ttu-id="32585-337">Valeur indiquant où un bot prend en charge les appels vidéo.</span><span class="sxs-lookup"><span data-stu-id="32585-337">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="32585-338">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="32585-338">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="32585-339">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="32585-339">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="32585-340">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="32585-340">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="32585-341">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="32585-341">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="32585-342">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="32585-342">bots.commandLists</span></span>

<span data-ttu-id="32585-343">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="32585-343">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="32585-344">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-344">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="32585-345">Pour plus [d’informations,](~/bots/how-to/create-a-bot-commands-menu.md) voir les menus du bot.</span><span class="sxs-lookup"><span data-stu-id="32585-345">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="32585-346">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-346">Name</span></span>| <span data-ttu-id="32585-347">Type</span><span class="sxs-lookup"><span data-stu-id="32585-347">Type</span></span>| <span data-ttu-id="32585-348">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-348">Maximum size</span></span> | <span data-ttu-id="32585-349">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-349">Required</span></span> | <span data-ttu-id="32585-350">Description</span><span class="sxs-lookup"><span data-stu-id="32585-350">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="32585-351">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-351">array of enums</span></span>|<span data-ttu-id="32585-352">3</span><span class="sxs-lookup"><span data-stu-id="32585-352">3</span></span>|<span data-ttu-id="32585-353">✔</span><span class="sxs-lookup"><span data-stu-id="32585-353">✔</span></span>|<span data-ttu-id="32585-354">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="32585-354">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="32585-355">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="32585-355">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="32585-356">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-356">array of objects</span></span>|<span data-ttu-id="32585-357">10 </span><span class="sxs-lookup"><span data-stu-id="32585-357">10</span></span>|<span data-ttu-id="32585-358">✔</span><span class="sxs-lookup"><span data-stu-id="32585-358">✔</span></span>|<span data-ttu-id="32585-359">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="32585-359">An array of commands the bot supports:</span></span><br><span data-ttu-id="32585-360">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="32585-360">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="32585-361">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="32585-361">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="32585-362">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="32585-362">bots.commandLists.commands</span></span>

|<span data-ttu-id="32585-363">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-363">Name</span></span>| <span data-ttu-id="32585-364">Type</span><span class="sxs-lookup"><span data-stu-id="32585-364">Type</span></span>| <span data-ttu-id="32585-365">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-365">Maximum size</span></span> | <span data-ttu-id="32585-366">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-366">Required</span></span> | <span data-ttu-id="32585-367">Description</span><span class="sxs-lookup"><span data-stu-id="32585-367">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="32585-368">title</span><span class="sxs-lookup"><span data-stu-id="32585-368">title</span></span>|<span data-ttu-id="32585-369">string</span><span class="sxs-lookup"><span data-stu-id="32585-369">string</span></span>|<span data-ttu-id="32585-370">12 </span><span class="sxs-lookup"><span data-stu-id="32585-370">12</span></span>|<span data-ttu-id="32585-371">✔</span><span class="sxs-lookup"><span data-stu-id="32585-371">✔</span></span>|<span data-ttu-id="32585-372">Nom de la commande du bot</span><span class="sxs-lookup"><span data-stu-id="32585-372">The bot command name</span></span>|
|<span data-ttu-id="32585-373">description</span><span class="sxs-lookup"><span data-stu-id="32585-373">description</span></span>|<span data-ttu-id="32585-374">string</span><span class="sxs-lookup"><span data-stu-id="32585-374">string</span></span>|<span data-ttu-id="32585-375">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-375">128 characters</span></span>|<span data-ttu-id="32585-376">✔</span><span class="sxs-lookup"><span data-stu-id="32585-376">✔</span></span>|<span data-ttu-id="32585-377">Description de texte simple ou exemple de syntaxe de commande et de ses arguments.</span><span class="sxs-lookup"><span data-stu-id="32585-377">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="32585-378">connecteurs</span><span class="sxs-lookup"><span data-stu-id="32585-378">connectors</span></span>

<span data-ttu-id="32585-379">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="32585-379">**Optional** — array</span></span>

<span data-ttu-id="32585-380">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-380">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="32585-381">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="32585-381">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="32585-382">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="32585-382">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="32585-383">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-383">Name</span></span>| <span data-ttu-id="32585-384">Type</span><span class="sxs-lookup"><span data-stu-id="32585-384">Type</span></span>| <span data-ttu-id="32585-385">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-385">Maximum size</span></span> | <span data-ttu-id="32585-386">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-386">Required</span></span> | <span data-ttu-id="32585-387">Description</span><span class="sxs-lookup"><span data-stu-id="32585-387">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="32585-388">string</span><span class="sxs-lookup"><span data-stu-id="32585-388">string</span></span>|<span data-ttu-id="32585-389">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-389">2048 characters</span></span>|<span data-ttu-id="32585-390">✔</span><span class="sxs-lookup"><span data-stu-id="32585-390">✔</span></span>|<span data-ttu-id="32585-391">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="32585-391">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="32585-392">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="32585-392">array of enums</span></span>|<span data-ttu-id="32585-393">1</span><span class="sxs-lookup"><span data-stu-id="32585-393">1</span></span>|<span data-ttu-id="32585-394">✔</span><span class="sxs-lookup"><span data-stu-id="32585-394">✔</span></span>|<span data-ttu-id="32585-395">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="32585-395">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="32585-396">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="32585-396">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="32585-397">string</span><span class="sxs-lookup"><span data-stu-id="32585-397">string</span></span>|<span data-ttu-id="32585-398">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-398">64 characters</span></span>|<span data-ttu-id="32585-399">✔</span><span class="sxs-lookup"><span data-stu-id="32585-399">✔</span></span>|<span data-ttu-id="32585-400">Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="32585-400">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="32585-401">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="32585-401">composeExtensions</span></span>

<span data-ttu-id="32585-402">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="32585-402">**Optional** — array</span></span>

<span data-ttu-id="32585-403">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-403">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="32585-404">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="32585-404">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="32585-405">L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="32585-405">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="32585-406">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="32585-406">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="32585-407">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-407">Name</span></span>| <span data-ttu-id="32585-408">Type</span><span class="sxs-lookup"><span data-stu-id="32585-408">Type</span></span> | <span data-ttu-id="32585-409">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-409">Maximum Size</span></span> | <span data-ttu-id="32585-410">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="32585-410">Required</span></span> | <span data-ttu-id="32585-411">Description</span><span class="sxs-lookup"><span data-stu-id="32585-411">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="32585-412">string</span><span class="sxs-lookup"><span data-stu-id="32585-412">string</span></span>|<span data-ttu-id="32585-413">64</span><span class="sxs-lookup"><span data-stu-id="32585-413">64</span></span>|<span data-ttu-id="32585-414">✔</span><span class="sxs-lookup"><span data-stu-id="32585-414">✔</span></span>|<span data-ttu-id="32585-415">ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="32585-415">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="32585-416">Cela peut être identique à l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="32585-416">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="32585-417">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-417">array of objects</span></span>|<span data-ttu-id="32585-418">10 </span><span class="sxs-lookup"><span data-stu-id="32585-418">10</span></span>|<span data-ttu-id="32585-419">✔</span><span class="sxs-lookup"><span data-stu-id="32585-419">✔</span></span>|<span data-ttu-id="32585-420">Tableau de commandes pris en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="32585-420">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="32585-421">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-421">boolean</span></span>|||<span data-ttu-id="32585-422">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32585-422">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="32585-423">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="32585-423">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="32585-424">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-424">array of Objects</span></span>|<span data-ttu-id="32585-425">5 </span><span class="sxs-lookup"><span data-stu-id="32585-425">5</span></span>||<span data-ttu-id="32585-426">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="32585-426">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="32585-427">string</span><span class="sxs-lookup"><span data-stu-id="32585-427">string</span></span>|||<span data-ttu-id="32585-428">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="32585-428">The type of message handler.</span></span> <span data-ttu-id="32585-429">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="32585-429">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="32585-430">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="32585-430">array of Strings</span></span>|||<span data-ttu-id="32585-431">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="32585-431">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="32585-432">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="32585-432">composeExtensions.commands</span></span>

<span data-ttu-id="32585-433">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="32585-433">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="32585-434">Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32585-434">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="32585-435">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="32585-435">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="32585-436">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="32585-436">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="32585-437">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-437">Name</span></span>| <span data-ttu-id="32585-438">Type</span><span class="sxs-lookup"><span data-stu-id="32585-438">Type</span></span>| <span data-ttu-id="32585-439">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-439">Maximum size</span></span> | <span data-ttu-id="32585-440">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-440">Required</span></span> | <span data-ttu-id="32585-441">Description</span><span class="sxs-lookup"><span data-stu-id="32585-441">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="32585-442">string</span><span class="sxs-lookup"><span data-stu-id="32585-442">string</span></span>|<span data-ttu-id="32585-443">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-443">64 characters</span></span>|<span data-ttu-id="32585-444">✔</span><span class="sxs-lookup"><span data-stu-id="32585-444">✔</span></span>|<span data-ttu-id="32585-445">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="32585-445">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="32585-446">string</span><span class="sxs-lookup"><span data-stu-id="32585-446">string</span></span>|<span data-ttu-id="32585-447">32 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-447">32 characters</span></span>|<span data-ttu-id="32585-448">✔</span><span class="sxs-lookup"><span data-stu-id="32585-448">✔</span></span>|<span data-ttu-id="32585-449">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="32585-449">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="32585-450">string</span><span class="sxs-lookup"><span data-stu-id="32585-450">string</span></span>|<span data-ttu-id="32585-451">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-451">64 characters</span></span>||<span data-ttu-id="32585-452">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="32585-452">Type of the command.</span></span> <span data-ttu-id="32585-453">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="32585-453">One of `query` or `action`.</span></span> <span data-ttu-id="32585-454">Par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="32585-454">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="32585-455">string</span><span class="sxs-lookup"><span data-stu-id="32585-455">string</span></span>|<span data-ttu-id="32585-456">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-456">128 characters</span></span>||<span data-ttu-id="32585-457">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="32585-457">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="32585-458">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-458">boolean</span></span>|||<span data-ttu-id="32585-459">Une valeur booléle indique si la commande s’exécute initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="32585-459">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="32585-460">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="32585-460">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="32585-461">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="32585-461">array of Strings</span></span>|<span data-ttu-id="32585-462">3</span><span class="sxs-lookup"><span data-stu-id="32585-462">3</span></span>||<span data-ttu-id="32585-463">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="32585-463">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="32585-464">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="32585-464">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="32585-465">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="32585-465">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="32585-466">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="32585-466">boolean</span></span>|||<span data-ttu-id="32585-467">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="32585-467">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="32585-468">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="32585-468">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="32585-469">objet</span><span class="sxs-lookup"><span data-stu-id="32585-469">object</span></span>|||<span data-ttu-id="32585-470">Spécifiez le module de tâche à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="32585-470">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="32585-471">string</span><span class="sxs-lookup"><span data-stu-id="32585-471">string</span></span>|<span data-ttu-id="32585-472">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-472">64 characters</span></span>||<span data-ttu-id="32585-473">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="32585-473">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="32585-474">string</span><span class="sxs-lookup"><span data-stu-id="32585-474">string</span></span>|||<span data-ttu-id="32585-475">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="32585-475">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="32585-476">string</span><span class="sxs-lookup"><span data-stu-id="32585-476">string</span></span>|||<span data-ttu-id="32585-477">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="32585-477">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="32585-478">string</span><span class="sxs-lookup"><span data-stu-id="32585-478">string</span></span>|||<span data-ttu-id="32585-479">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="32585-479">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="32585-480">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-480">array of object</span></span>|<span data-ttu-id="32585-481">5 éléments</span><span class="sxs-lookup"><span data-stu-id="32585-481">5 items</span></span>|<span data-ttu-id="32585-482">✔</span><span class="sxs-lookup"><span data-stu-id="32585-482">✔</span></span>|<span data-ttu-id="32585-483">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="32585-483">The list of parameters the command takes.</span></span> <span data-ttu-id="32585-484">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="32585-484">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="32585-485">string</span><span class="sxs-lookup"><span data-stu-id="32585-485">string</span></span>|<span data-ttu-id="32585-486">64 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-486">64 characters</span></span>|<span data-ttu-id="32585-487">✔</span><span class="sxs-lookup"><span data-stu-id="32585-487">✔</span></span>|<span data-ttu-id="32585-488">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="32585-488">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="32585-489">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32585-489">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="32585-490">string</span><span class="sxs-lookup"><span data-stu-id="32585-490">string</span></span>|<span data-ttu-id="32585-491">32 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-491">32 characters</span></span>|<span data-ttu-id="32585-492">✔</span><span class="sxs-lookup"><span data-stu-id="32585-492">✔</span></span>|<span data-ttu-id="32585-493">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="32585-493">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="32585-494">string</span><span class="sxs-lookup"><span data-stu-id="32585-494">string</span></span>|<span data-ttu-id="32585-495">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-495">128 characters</span></span>||<span data-ttu-id="32585-496">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="32585-496">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="32585-497">string</span><span class="sxs-lookup"><span data-stu-id="32585-497">string</span></span>|<span data-ttu-id="32585-498">512 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-498">512 characters</span></span>||<span data-ttu-id="32585-499">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="32585-499">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="32585-500">string</span><span class="sxs-lookup"><span data-stu-id="32585-500">string</span></span>|<span data-ttu-id="32585-501">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-501">128 characters</span></span>||<span data-ttu-id="32585-502">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="32585-502">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="32585-503">L’une `text, textarea, number, date, time, toggle, choiceset` des .</span><span class="sxs-lookup"><span data-stu-id="32585-503">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="32585-504">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-504">array of objects</span></span>|<span data-ttu-id="32585-505">10 éléments</span><span class="sxs-lookup"><span data-stu-id="32585-505">10 items</span></span>||<span data-ttu-id="32585-506">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="32585-506">The choice options for the`choiceset`.</span></span> <span data-ttu-id="32585-507">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="32585-507">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="32585-508">string</span><span class="sxs-lookup"><span data-stu-id="32585-508">string</span></span>|<span data-ttu-id="32585-509">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-509">128 characters</span></span>|<span data-ttu-id="32585-510">✔</span><span class="sxs-lookup"><span data-stu-id="32585-510">✔</span></span>|<span data-ttu-id="32585-511">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="32585-511">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="32585-512">string</span><span class="sxs-lookup"><span data-stu-id="32585-512">string</span></span>|<span data-ttu-id="32585-513">512 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-513">512 characters</span></span>|<span data-ttu-id="32585-514">✔</span><span class="sxs-lookup"><span data-stu-id="32585-514">✔</span></span>|<span data-ttu-id="32585-515">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="32585-515">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="32585-516">autorisations</span><span class="sxs-lookup"><span data-stu-id="32585-516">permissions</span></span>

<span data-ttu-id="32585-517">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="32585-517">**Optional** — array of strings</span></span>

<span data-ttu-id="32585-518">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` fonctionne l’extension.</span><span class="sxs-lookup"><span data-stu-id="32585-518">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="32585-519">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="32585-519">The following options are non-exclusive:</span></span>

* <span data-ttu-id="32585-520">`identity`&emsp;Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="32585-520">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="32585-521">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="32585-521">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="32585-522">Si vous modifiez ces autorisations pendant la mise à jour de l’application, vos utilisateurs répètent le processus de consentement après avoir exécuté l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="32585-522">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="32585-523">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) Mise à jour de votre application.</span><span class="sxs-lookup"><span data-stu-id="32585-523">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="32585-524">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="32585-524">devicePermissions</span></span>

<span data-ttu-id="32585-525">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="32585-525">**Optional** — array of strings</span></span>

<span data-ttu-id="32585-526">Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès.</span><span class="sxs-lookup"><span data-stu-id="32585-526">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="32585-527">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="32585-527">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="32585-528">validDomains</span><span class="sxs-lookup"><span data-stu-id="32585-528">validDomains</span></span>

<span data-ttu-id="32585-529">**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué</span><span class="sxs-lookup"><span data-stu-id="32585-529">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="32585-530">Liste des domaines valides pour les sites web que l’application s’attend à charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-530">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="32585-531">Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="32585-531">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="32585-532">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="32585-532">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="32585-533">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="32585-533">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="32585-534">Il **n’est** pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="32585-534">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="32585-535">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="32585-535">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="32585-536">Les applications Teams qui nécessitent leurs propres URL sharepoint pour fonctionner bien incluent « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="32585-536">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32585-537">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="32585-537">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="32585-538">Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="32585-538">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="32585-539">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="32585-539">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="32585-540">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="32585-540">webApplicationInfo</span></span>

<span data-ttu-id="32585-541">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-541">**Optional** — object</span></span>

<span data-ttu-id="32585-542">Fournissez votre ID d’application Azure Active Directory (AAD) et des informations Microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application.</span><span class="sxs-lookup"><span data-stu-id="32585-542">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="32585-543">Si votre application est inscrite dans AAD, vous devez fournir l’ID de l’application, afin que les administrateurs peuvent facilement passer en revue les autorisations et accorder leur consentement dans le Centre d’administration Teams.</span><span class="sxs-lookup"><span data-stu-id="32585-543">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="32585-544">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-544">Name</span></span>| <span data-ttu-id="32585-545">Type</span><span class="sxs-lookup"><span data-stu-id="32585-545">Type</span></span>| <span data-ttu-id="32585-546">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-546">Maximum size</span></span> | <span data-ttu-id="32585-547">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-547">Required</span></span> | <span data-ttu-id="32585-548">Description</span><span class="sxs-lookup"><span data-stu-id="32585-548">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="32585-549">string</span><span class="sxs-lookup"><span data-stu-id="32585-549">string</span></span>|<span data-ttu-id="32585-550">36 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-550">36 characters</span></span>|<span data-ttu-id="32585-551">✔</span><span class="sxs-lookup"><span data-stu-id="32585-551">✔</span></span>|<span data-ttu-id="32585-552">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="32585-552">AAD application id of the app.</span></span> <span data-ttu-id="32585-553">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="32585-553">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="32585-554">string</span><span class="sxs-lookup"><span data-stu-id="32585-554">string</span></span>|<span data-ttu-id="32585-555">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-555">2048 characters</span></span>|<span data-ttu-id="32585-556">✔</span><span class="sxs-lookup"><span data-stu-id="32585-556">✔</span></span>|<span data-ttu-id="32585-557">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="32585-557">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="32585-558">**REMARQUE :** Si vous n’utilisez pas l’oD SSO, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, pour éviter une réponse https://notapplicable d’erreur.</span><span class="sxs-lookup"><span data-stu-id="32585-558">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="32585-559">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="32585-559">array of strings</span></span>|<span data-ttu-id="32585-560">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-560">128 characters</span></span>||<span data-ttu-id="32585-561">Spécifiez le consentement précis [spécifique à une ressource.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="32585-561">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="32585-562">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="32585-562">showLoadingIndicator</span></span>

<span data-ttu-id="32585-563">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="32585-563">**Optional** — boolean</span></span>

<span data-ttu-id="32585-564">Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="32585-564">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="32585-565">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="32585-565">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="32585-566">Si vous sélectionnez true dans le manifeste de votre application, pour charger la page correctement, modifiez les pages de contenu de vos onglets et modules de tâche comme décrit dans Afficher un document d’indicateur de chargement `showLoadingIndicator` natif. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="32585-566">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="32585-567">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="32585-567">isFullScreen</span></span>

 <span data-ttu-id="32585-568">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="32585-568">**Optional** — boolean</span></span>

<span data-ttu-id="32585-569">Indiquez l’endroit où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="32585-569">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="32585-570">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="32585-570">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="32585-571">activités</span><span class="sxs-lookup"><span data-stu-id="32585-571">activities</span></span>

<span data-ttu-id="32585-572">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="32585-572">**Optional** — object</span></span>

<span data-ttu-id="32585-573">Définissez les propriétés que votre application utilise pour publier un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32585-573">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="32585-574">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-574">Name</span></span>| <span data-ttu-id="32585-575">Type</span><span class="sxs-lookup"><span data-stu-id="32585-575">Type</span></span>| <span data-ttu-id="32585-576">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-576">Maximum size</span></span> | <span data-ttu-id="32585-577">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-577">Required</span></span> | <span data-ttu-id="32585-578">Description</span><span class="sxs-lookup"><span data-stu-id="32585-578">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="32585-579">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="32585-579">array of Objects</span></span>|<span data-ttu-id="32585-580">128 éléments</span><span class="sxs-lookup"><span data-stu-id="32585-580">128 items</span></span>| | <span data-ttu-id="32585-581">Fournissez les types d’activités que votre application peut publier dans un flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="32585-581">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="32585-582">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="32585-582">activities.activityTypes</span></span>

|<span data-ttu-id="32585-583">Nom</span><span class="sxs-lookup"><span data-stu-id="32585-583">Name</span></span>| <span data-ttu-id="32585-584">Type</span><span class="sxs-lookup"><span data-stu-id="32585-584">Type</span></span>| <span data-ttu-id="32585-585">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="32585-585">Maximum size</span></span> | <span data-ttu-id="32585-586">Requis</span><span class="sxs-lookup"><span data-stu-id="32585-586">Required</span></span> | <span data-ttu-id="32585-587">Description</span><span class="sxs-lookup"><span data-stu-id="32585-587">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="32585-588">string</span><span class="sxs-lookup"><span data-stu-id="32585-588">string</span></span>|<span data-ttu-id="32585-589">32 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-589">32 characters</span></span>|<span data-ttu-id="32585-590">✔</span><span class="sxs-lookup"><span data-stu-id="32585-590">✔</span></span>|<span data-ttu-id="32585-591">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="32585-591">The notification type.</span></span> <span data-ttu-id="32585-592">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="32585-592">*See below*.</span></span>|
|`description`|<span data-ttu-id="32585-593">string</span><span class="sxs-lookup"><span data-stu-id="32585-593">string</span></span>|<span data-ttu-id="32585-594">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-594">128 characters</span></span>|<span data-ttu-id="32585-595">✔</span><span class="sxs-lookup"><span data-stu-id="32585-595">✔</span></span>|<span data-ttu-id="32585-596">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="32585-596">A brief description of the notification.</span></span> <span data-ttu-id="32585-597">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="32585-597">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="32585-598">string</span><span class="sxs-lookup"><span data-stu-id="32585-598">string</span></span>|<span data-ttu-id="32585-599">128 caractères</span><span class="sxs-lookup"><span data-stu-id="32585-599">128 characters</span></span>|<span data-ttu-id="32585-600">✔</span><span class="sxs-lookup"><span data-stu-id="32585-600">✔</span></span>|<span data-ttu-id="32585-601">Ex: « {actor} created task {taskId} for you »</span><span class="sxs-lookup"><span data-stu-id="32585-601">Ex: "{actor} created task {taskId} for you"</span></span>|

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


