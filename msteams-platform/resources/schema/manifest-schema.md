---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste pour Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: schéma de manifeste teams
ms.openlocfilehash: d8427d23ba2caa73cecd173f6d1ef0d041252b3b
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710626"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="dfce5-104">Référence : schéma de manifeste pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dfce5-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="dfce5-105">Le Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="dfce5-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="dfce5-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="dfce5-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="dfce5-107">Les versions précédentes 1.0, 1.1,..., 1.6, etc., sont également pris en charge (à l’aide de « v1.x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="dfce5-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="dfce5-108">Pour plus d’informations sur les modifications apportées dans chaque version, voir [le journal des modifications du manifeste.](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)</span><span class="sxs-lookup"><span data-stu-id="dfce5-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="dfce5-109">L’exemple de schéma suivant montre toutes les options d’extensibilité :</span><span class="sxs-lookup"><span data-stu-id="dfce5-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="dfce5-110">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="dfce5-110">Sample full manifest</span></span>

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

<span data-ttu-id="dfce5-111">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfce5-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="dfce5-112">$schema</span><span class="sxs-lookup"><span data-stu-id="dfce5-112">$schema</span></span>

<span data-ttu-id="dfce5-113">Chaîne facultative, mais recommandée</span><span class="sxs-lookup"><span data-stu-id="dfce5-113">Optional, but recommended — string</span></span>

<span data-ttu-id="dfce5-114">L https:// URL qui fait référence au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="dfce5-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="dfce5-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="dfce5-115">manifestVersion</span></span>

<span data-ttu-id="dfce5-116">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="dfce5-116">**Required** — string</span></span>

<span data-ttu-id="dfce5-117">Version du schéma de manifeste que ce manifeste utilise.</span><span class="sxs-lookup"><span data-stu-id="dfce5-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="dfce5-118">Elle doit être 1,10.</span><span class="sxs-lookup"><span data-stu-id="dfce5-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="dfce5-119">version</span><span class="sxs-lookup"><span data-stu-id="dfce5-119">version</span></span>

<span data-ttu-id="dfce5-120">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="dfce5-120">**Required** — string</span></span>

<span data-ttu-id="dfce5-121">Version d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="dfce5-121">The version of a specific app.</span></span> <span data-ttu-id="dfce5-122">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="dfce5-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="dfce5-123">De cette façon, lorsque le nouveau manifeste est installé, il se place sur le manifeste existant et l’utilisateur reçoit la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dfce5-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="dfce5-124">Si cette application a été soumise au Store, le nouveau manifeste doit être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="dfce5-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="dfce5-125">Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour quelques heures après l’approbation du manifeste.</span><span class="sxs-lookup"><span data-stu-id="dfce5-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="dfce5-126">Si l’application demande des autorisations, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="dfce5-127">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="dfce5-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="dfce5-128">id</span><span class="sxs-lookup"><span data-stu-id="dfce5-128">id</span></span>

<span data-ttu-id="dfce5-129">**Obligatoire** — ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="dfce5-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="dfce5-130">L’ID est un identificateur unique généré par Microsoft pour l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="dfce5-131">Vous avez un ID si votre bot est inscrit via le Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dfce5-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="dfce5-132">Vous devez entrer l’ID ici.</span><span class="sxs-lookup"><span data-stu-id="dfce5-132">You must enter the ID here.</span></span> <span data-ttu-id="dfce5-133">Sinon, vous devez générer un nouvel ID sur le portail [d’inscription des applications Microsoft.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="dfce5-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="dfce5-134">Utilisez le même ID si vous ajoutez un bot.</span><span class="sxs-lookup"><span data-stu-id="dfce5-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="dfce5-135">Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="dfce5-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="dfce5-136">developer</span><span class="sxs-lookup"><span data-stu-id="dfce5-136">developer</span></span>

<span data-ttu-id="dfce5-137">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-137">**Required** — object</span></span>

<span data-ttu-id="dfce5-138">Spécifie des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="dfce5-138">Specifies information about your company.</span></span> <span data-ttu-id="dfce5-139">Pour les applications envoyées au Teams store, ces valeurs doivent correspondre aux informations de votre listing dans le Windows Store.</span><span class="sxs-lookup"><span data-stu-id="dfce5-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="dfce5-140">Pour plus d’informations, voir les [Teams de publication du Store.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="dfce5-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="dfce5-141">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-141">Name</span></span>| <span data-ttu-id="dfce5-142">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-142">Maximum size</span></span> | <span data-ttu-id="dfce5-143">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-143">Required</span></span> | <span data-ttu-id="dfce5-144">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="dfce5-145">32 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-145">32 characters</span></span>|<span data-ttu-id="dfce5-146">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-146">✔</span></span>|<span data-ttu-id="dfce5-147">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="dfce5-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-148">2048 characters</span></span>|<span data-ttu-id="dfce5-149">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-149">✔</span></span>|<span data-ttu-id="dfce5-150">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="dfce5-151">Ce lien doit prendre les utilisateurs vers votre entreprise ou la page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="dfce5-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="dfce5-152">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-152">2048 characters</span></span>|<span data-ttu-id="dfce5-153">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-153">✔</span></span>|<span data-ttu-id="dfce5-154">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="dfce5-155">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-155">2048 characters</span></span>|<span data-ttu-id="dfce5-156">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-156">✔</span></span>|<span data-ttu-id="dfce5-157">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="dfce5-158">10 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-158">10 characters</span></span>| |<span data-ttu-id="dfce5-159">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="dfce5-160">name</span><span class="sxs-lookup"><span data-stu-id="dfce5-160">name</span></span>

<span data-ttu-id="dfce5-161">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-161">**Required** — object</span></span>

<span data-ttu-id="dfce5-162">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’Teams expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="dfce5-163">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="dfce5-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="dfce5-164">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="dfce5-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="dfce5-165">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-165">Name</span></span>| <span data-ttu-id="dfce5-166">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-166">Maximum size</span></span> | <span data-ttu-id="dfce5-167">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-167">Required</span></span> | <span data-ttu-id="dfce5-168">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="dfce5-169">30 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-169">30 characters</span></span>|<span data-ttu-id="dfce5-170">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-170">✔</span></span>|<span data-ttu-id="dfce5-171">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="dfce5-172">100 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-172">100 characters</span></span>||<span data-ttu-id="dfce5-173">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="dfce5-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="dfce5-174">description</span><span class="sxs-lookup"><span data-stu-id="dfce5-174">description</span></span>

<span data-ttu-id="dfce5-175">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-175">**Required** — object</span></span>

<span data-ttu-id="dfce5-176">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dfce5-176">Describes your app to users.</span></span> <span data-ttu-id="dfce5-177">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="dfce5-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="dfce5-178">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="dfce5-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="dfce5-179">Vous devez le noter dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="dfce5-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="dfce5-180">Les valeurs `short` de et doivent être `full` différentes.</span><span class="sxs-lookup"><span data-stu-id="dfce5-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="dfce5-181">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="dfce5-182">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-182">Name</span></span>| <span data-ttu-id="dfce5-183">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-183">Maximum size</span></span> | <span data-ttu-id="dfce5-184">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-184">Required</span></span> | <span data-ttu-id="dfce5-185">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="dfce5-186">80 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-186">80 characters</span></span>|<span data-ttu-id="dfce5-187">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-187">✔</span></span>|<span data-ttu-id="dfce5-188">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="dfce5-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="dfce5-189">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-189">4000 characters</span></span>|<span data-ttu-id="dfce5-190">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-190">✔</span></span>|<span data-ttu-id="dfce5-191">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="dfce5-192">packageName</span><span class="sxs-lookup"><span data-stu-id="dfce5-192">packageName</span></span>

<span data-ttu-id="dfce5-193">**Facultatif —** chaîne</span><span class="sxs-lookup"><span data-stu-id="dfce5-193">**Optional** — string</span></span>

<span data-ttu-id="dfce5-194">Identificateur unique de l’application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="dfce5-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="dfce5-195">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="dfce5-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="dfce5-196">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="dfce5-196">localizationInfo</span></span>

<span data-ttu-id="dfce5-197">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-197">**Optional** — object</span></span>

<span data-ttu-id="dfce5-198">Permet la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="dfce5-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="dfce5-199">Pour plus d’informations, [voir localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="dfce5-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="dfce5-200">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-200">Name</span></span>| <span data-ttu-id="dfce5-201">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-201">Maximum size</span></span> | <span data-ttu-id="dfce5-202">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-202">Required</span></span> | <span data-ttu-id="dfce5-203">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="dfce5-204">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-204">✔</span></span>|<span data-ttu-id="dfce5-205">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="dfce5-206">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="dfce5-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="dfce5-207">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="dfce5-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="dfce5-208">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-208">Name</span></span>| <span data-ttu-id="dfce5-209">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-209">Maximum size</span></span> | <span data-ttu-id="dfce5-210">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-210">Required</span></span> | <span data-ttu-id="dfce5-211">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="dfce5-212">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-212">✔</span></span>|<span data-ttu-id="dfce5-213">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="dfce5-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="dfce5-214">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-214">✔</span></span>|<span data-ttu-id="dfce5-215">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="dfce5-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="dfce5-216">icons</span><span class="sxs-lookup"><span data-stu-id="dfce5-216">icons</span></span>

<span data-ttu-id="dfce5-217">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-217">**Required** — object</span></span>

<span data-ttu-id="dfce5-218">Icônes utilisées dans l’Teams app.</span><span class="sxs-lookup"><span data-stu-id="dfce5-218">Icons used within the Teams app.</span></span> <span data-ttu-id="dfce5-219">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="dfce5-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="dfce5-220">Pour plus [d’informations,](../../concepts/build-and-test/apps-package.md#app-icons) voir Icônes.</span><span class="sxs-lookup"><span data-stu-id="dfce5-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="dfce5-221">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-221">Name</span></span>| <span data-ttu-id="dfce5-222">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-222">Maximum size</span></span> | <span data-ttu-id="dfce5-223">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-223">Required</span></span> | <span data-ttu-id="dfce5-224">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="dfce5-225">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="dfce5-225">32 x 32 pixels</span></span>|<span data-ttu-id="dfce5-226">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-226">✔</span></span>|<span data-ttu-id="dfce5-227">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="dfce5-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="dfce5-228">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="dfce5-228">192 x 192 pixels</span></span>|<span data-ttu-id="dfce5-229">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-229">✔</span></span>|<span data-ttu-id="dfce5-230">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="dfce5-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="dfce5-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="dfce5-231">accentColor</span></span>

<span data-ttu-id="dfce5-232">**Facultatif** — Code de couleur HTML Hex</span><span class="sxs-lookup"><span data-stu-id="dfce5-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="dfce5-233">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="dfce5-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="dfce5-234">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="dfce5-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="dfce5-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="dfce5-235">configurableTabs</span></span>

<span data-ttu-id="dfce5-236">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-236">**Optional** — array</span></span>

<span data-ttu-id="dfce5-237">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="dfce5-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="dfce5-238">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams et vous pouvez configurer les mêmes onglets plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="dfce5-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="dfce5-239">Toutefois, vous ne pouvez la définir dans le manifeste qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="dfce5-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="dfce5-240">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-240">Name</span></span>| <span data-ttu-id="dfce5-241">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-241">Type</span></span>| <span data-ttu-id="dfce5-242">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-242">Maximum size</span></span> | <span data-ttu-id="dfce5-243">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-243">Required</span></span> | <span data-ttu-id="dfce5-244">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="dfce5-245">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-245">string</span></span>|<span data-ttu-id="dfce5-246">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-246">2048 characters</span></span>|<span data-ttu-id="dfce5-247">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-247">✔</span></span>|<span data-ttu-id="dfce5-248">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="dfce5-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="dfce5-249">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-249">array of enums</span></span>|<span data-ttu-id="dfce5-250">1</span><span class="sxs-lookup"><span data-stu-id="dfce5-250">1</span></span>|<span data-ttu-id="dfce5-251">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-251">✔</span></span>|<span data-ttu-id="dfce5-252">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="dfce5-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="dfce5-253">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-253">boolean</span></span>|||<span data-ttu-id="dfce5-254">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="dfce5-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="dfce5-255">Valeur par défaut **: true**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="dfce5-256">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-256">array of enums</span></span>|<span data-ttu-id="dfce5-257">6 </span><span class="sxs-lookup"><span data-stu-id="dfce5-257">6</span></span>||<span data-ttu-id="dfce5-258">Ensemble `contextItem` d’étendues où un [onglet est pris en charge.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="dfce5-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="dfce5-259">Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="dfce5-260">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-260">string</span></span>|<span data-ttu-id="dfce5-261">2048</span><span class="sxs-lookup"><span data-stu-id="dfce5-261">2048</span></span>||<span data-ttu-id="dfce5-262">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dfce5-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="dfce5-263">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="dfce5-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="dfce5-264">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-264">array of enums</span></span>|<span data-ttu-id="dfce5-265">1</span><span class="sxs-lookup"><span data-stu-id="dfce5-265">1</span></span>||<span data-ttu-id="dfce5-266">Définit la façon dont votre onglet est mis à disposition dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dfce5-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="dfce5-267">Les options sont `sharePointFullPage` les `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="dfce5-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="dfce5-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="dfce5-268">staticTabs</span></span>

<span data-ttu-id="dfce5-269">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-269">**Optional** — array</span></span>

<span data-ttu-id="dfce5-270">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="dfce5-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="dfce5-271">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="dfce5-272">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dfce5-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="dfce5-273">Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="dfce5-274">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="dfce5-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="dfce5-275">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-275">Name</span></span>| <span data-ttu-id="dfce5-276">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-276">Type</span></span>| <span data-ttu-id="dfce5-277">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-277">Maximum size</span></span> | <span data-ttu-id="dfce5-278">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-278">Required</span></span> | <span data-ttu-id="dfce5-279">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="dfce5-280">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-280">string</span></span>|<span data-ttu-id="dfce5-281">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-281">64 characters</span></span>|<span data-ttu-id="dfce5-282">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-282">✔</span></span>|<span data-ttu-id="dfce5-283">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="dfce5-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="dfce5-284">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-284">string</span></span>|<span data-ttu-id="dfce5-285">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-285">128 characters</span></span>|<span data-ttu-id="dfce5-286">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-286">✔</span></span>|<span data-ttu-id="dfce5-287">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="dfce5-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="dfce5-288">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-288">string</span></span>||<span data-ttu-id="dfce5-289">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-289">✔</span></span>|<span data-ttu-id="dfce5-290">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone Teams dessin.</span><span class="sxs-lookup"><span data-stu-id="dfce5-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="dfce5-291">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-291">string</span></span>|||<span data-ttu-id="dfce5-292">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="dfce5-293">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-293">string</span></span>|||<span data-ttu-id="dfce5-294">L https:// URL pointant vers les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="dfce5-295">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-295">array of enums</span></span>|<span data-ttu-id="dfce5-296">1</span><span class="sxs-lookup"><span data-stu-id="dfce5-296">1</span></span>|<span data-ttu-id="dfce5-297">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-297">✔</span></span>|<span data-ttu-id="dfce5-298">Actuellement, les onglets statiques ne peuvent prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="dfce5-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="dfce5-299">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-299">array of enums</span></span>| <span data-ttu-id="dfce5-300">2</span><span class="sxs-lookup"><span data-stu-id="dfce5-300">2</span></span>|| <span data-ttu-id="dfce5-301">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dfce5-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="dfce5-302">La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.</span><span class="sxs-lookup"><span data-stu-id="dfce5-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="dfce5-303">Si vos onglets nécessitent des informations contextielles pour afficher du contenu pertinent ou pour lancer un flux d’authentification, pour plus d’informations, voir Obtenir le contexte de [votre onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="dfce5-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="dfce5-304">bots</span><span class="sxs-lookup"><span data-stu-id="dfce5-304">bots</span></span>

<span data-ttu-id="dfce5-305">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-305">**Optional** — array</span></span>

<span data-ttu-id="dfce5-306">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="dfce5-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="dfce5-307">L’élément est un tableau (jusqu’à un seul élément actuellement un seul bot est autorisé par application) avec tous les &mdash; éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="dfce5-308">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="dfce5-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="dfce5-309">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-309">Name</span></span>| <span data-ttu-id="dfce5-310">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-310">Type</span></span>| <span data-ttu-id="dfce5-311">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-311">Maximum size</span></span> | <span data-ttu-id="dfce5-312">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-312">Required</span></span> | <span data-ttu-id="dfce5-313">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="dfce5-314">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-314">string</span></span>|<span data-ttu-id="dfce5-315">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-315">64 characters</span></span>|<span data-ttu-id="dfce5-316">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-316">✔</span></span>|<span data-ttu-id="dfce5-317">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="dfce5-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="dfce5-318">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="dfce5-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="dfce5-319">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-319">array of enums</span></span>|<span data-ttu-id="dfce5-320">3</span><span class="sxs-lookup"><span data-stu-id="dfce5-320">3</span></span>|<span data-ttu-id="dfce5-321">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-321">✔</span></span>|<span data-ttu-id="dfce5-322">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="dfce5-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="dfce5-323">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="dfce5-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="dfce5-324">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-324">boolean</span></span>|||<span data-ttu-id="dfce5-325">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="dfce5-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="dfce5-326">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="dfce5-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="dfce5-327">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-327">boolean</span></span>|||<span data-ttu-id="dfce5-328">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="dfce5-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="dfce5-329">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="dfce5-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="dfce5-330">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-330">boolean</span></span>|||<span data-ttu-id="dfce5-331">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="dfce5-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="dfce5-332">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="dfce5-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="dfce5-333">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-333">boolean</span></span>|||<span data-ttu-id="dfce5-334">Valeur indiquant où un bot prend en charge les appels audio.</span><span class="sxs-lookup"><span data-stu-id="dfce5-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="dfce5-335">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="dfce5-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="dfce5-336">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="dfce5-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="dfce5-337">Il est fourni à des fins de test et d’exploration uniquement et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="dfce5-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="dfce5-338">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="dfce5-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="dfce5-339">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-339">boolean</span></span>|||<span data-ttu-id="dfce5-340">Valeur indiquant où un bot prend en charge les appels vidéo.</span><span class="sxs-lookup"><span data-stu-id="dfce5-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="dfce5-341">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="dfce5-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="dfce5-342">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="dfce5-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="dfce5-343">Il est fourni à des fins de test et d’exploration uniquement et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="dfce5-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="dfce5-344">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="dfce5-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="dfce5-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="dfce5-345">bots.commandLists</span></span>

<span data-ttu-id="dfce5-346">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dfce5-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="dfce5-347">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="dfce5-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="dfce5-348">Pour plus [d’informations,](~/bots/how-to/create-a-bot-commands-menu.md) voir les menus du bot.</span><span class="sxs-lookup"><span data-stu-id="dfce5-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="dfce5-349">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-349">Name</span></span>| <span data-ttu-id="dfce5-350">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-350">Type</span></span>| <span data-ttu-id="dfce5-351">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-351">Maximum size</span></span> | <span data-ttu-id="dfce5-352">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-352">Required</span></span> | <span data-ttu-id="dfce5-353">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="dfce5-354">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-354">array of enums</span></span>|<span data-ttu-id="dfce5-355">3</span><span class="sxs-lookup"><span data-stu-id="dfce5-355">3</span></span>|<span data-ttu-id="dfce5-356">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-356">✔</span></span>|<span data-ttu-id="dfce5-357">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="dfce5-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="dfce5-358">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="dfce5-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="dfce5-359">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-359">array of objects</span></span>|<span data-ttu-id="dfce5-360">10</span><span class="sxs-lookup"><span data-stu-id="dfce5-360">10</span></span>|<span data-ttu-id="dfce5-361">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-361">✔</span></span>|<span data-ttu-id="dfce5-362">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="dfce5-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="dfce5-363">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="dfce5-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="dfce5-364">`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).</span><span class="sxs-lookup"><span data-stu-id="dfce5-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="dfce5-365">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="dfce5-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="dfce5-366">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-366">Name</span></span>| <span data-ttu-id="dfce5-367">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-367">Type</span></span>| <span data-ttu-id="dfce5-368">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-368">Maximum size</span></span> | <span data-ttu-id="dfce5-369">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-369">Required</span></span> | <span data-ttu-id="dfce5-370">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="dfce5-371">title</span><span class="sxs-lookup"><span data-stu-id="dfce5-371">title</span></span>|<span data-ttu-id="dfce5-372">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-372">string</span></span>|<span data-ttu-id="dfce5-373">12 </span><span class="sxs-lookup"><span data-stu-id="dfce5-373">12</span></span>|<span data-ttu-id="dfce5-374">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-374">✔</span></span>|<span data-ttu-id="dfce5-375">Nom de la commande du bot.</span><span class="sxs-lookup"><span data-stu-id="dfce5-375">The bot command name.</span></span>|
|<span data-ttu-id="dfce5-376">description</span><span class="sxs-lookup"><span data-stu-id="dfce5-376">description</span></span>|<span data-ttu-id="dfce5-377">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-377">string</span></span>|<span data-ttu-id="dfce5-378">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-378">128 characters</span></span>|<span data-ttu-id="dfce5-379">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-379">✔</span></span>|<span data-ttu-id="dfce5-380">Description de texte simple ou exemple de syntaxe de commande et de ses arguments.</span><span class="sxs-lookup"><span data-stu-id="dfce5-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="dfce5-381">connecteurs</span><span class="sxs-lookup"><span data-stu-id="dfce5-381">connectors</span></span>

<span data-ttu-id="dfce5-382">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-382">**Optional** — array</span></span>

<span data-ttu-id="dfce5-383">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="dfce5-384">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="dfce5-385">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="dfce5-386">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-386">Name</span></span>| <span data-ttu-id="dfce5-387">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-387">Type</span></span>| <span data-ttu-id="dfce5-388">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-388">Maximum size</span></span> | <span data-ttu-id="dfce5-389">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-389">Required</span></span> | <span data-ttu-id="dfce5-390">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="dfce5-391">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-391">string</span></span>|<span data-ttu-id="dfce5-392">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-392">2048 characters</span></span>|<span data-ttu-id="dfce5-393">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-393">✔</span></span>|<span data-ttu-id="dfce5-394">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="dfce5-395">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="dfce5-395">array of enums</span></span>|<span data-ttu-id="dfce5-396">1</span><span class="sxs-lookup"><span data-stu-id="dfce5-396">1</span></span>|<span data-ttu-id="dfce5-397">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-397">✔</span></span>|<span data-ttu-id="dfce5-398">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="dfce5-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="dfce5-399">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="dfce5-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="dfce5-400">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-400">string</span></span>|<span data-ttu-id="dfce5-401">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-401">64 characters</span></span>|<span data-ttu-id="dfce5-402">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-402">✔</span></span>|<span data-ttu-id="dfce5-403">Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="dfce5-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="dfce5-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="dfce5-404">composeExtensions</span></span>

<span data-ttu-id="dfce5-405">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-405">**Optional** — array</span></span>

<span data-ttu-id="dfce5-406">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="dfce5-407">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="dfce5-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="dfce5-408">L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="dfce5-409">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="dfce5-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="dfce5-410">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-410">Name</span></span>| <span data-ttu-id="dfce5-411">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-411">Type</span></span> | <span data-ttu-id="dfce5-412">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-412">Maximum Size</span></span> | <span data-ttu-id="dfce5-413">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="dfce5-413">Required</span></span> | <span data-ttu-id="dfce5-414">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="dfce5-415">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-415">string</span></span>|<span data-ttu-id="dfce5-416">64</span><span class="sxs-lookup"><span data-stu-id="dfce5-416">64</span></span>|<span data-ttu-id="dfce5-417">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-417">✔</span></span>|<span data-ttu-id="dfce5-418">ID d’application Microsoft unique pour le bot qui backs the messaging extension, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="dfce5-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="dfce5-419">Cela peut être identique à l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="dfce5-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="dfce5-420">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-420">array of objects</span></span>|<span data-ttu-id="dfce5-421">10</span><span class="sxs-lookup"><span data-stu-id="dfce5-421">10</span></span>|<span data-ttu-id="dfce5-422">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-422">✔</span></span>|<span data-ttu-id="dfce5-423">Tableau de commandes pris en charge par l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="dfce5-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="dfce5-424">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-424">boolean</span></span>|||<span data-ttu-id="dfce5-425">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="dfce5-426">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="dfce5-427">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-427">array of Objects</span></span>|<span data-ttu-id="dfce5-428">5 </span><span class="sxs-lookup"><span data-stu-id="dfce5-428">5</span></span>||<span data-ttu-id="dfce5-429">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="dfce5-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="dfce5-430">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-430">string</span></span>|||<span data-ttu-id="dfce5-431">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="dfce5-431">The type of message handler.</span></span> <span data-ttu-id="dfce5-432">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="dfce5-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="dfce5-433">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dfce5-433">array of Strings</span></span>|||<span data-ttu-id="dfce5-434">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="dfce5-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="dfce5-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="dfce5-435">composeExtensions.commands</span></span>

<span data-ttu-id="dfce5-436">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="dfce5-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="dfce5-437">Chaque commande s’affiche Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="dfce5-438">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="dfce5-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="dfce5-439">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="dfce5-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="dfce5-440">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-440">Name</span></span>| <span data-ttu-id="dfce5-441">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-441">Type</span></span>| <span data-ttu-id="dfce5-442">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-442">Maximum size</span></span> | <span data-ttu-id="dfce5-443">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-443">Required</span></span> | <span data-ttu-id="dfce5-444">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="dfce5-445">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-445">string</span></span>|<span data-ttu-id="dfce5-446">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-446">64 characters</span></span>|<span data-ttu-id="dfce5-447">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-447">✔</span></span>|<span data-ttu-id="dfce5-448">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="dfce5-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="dfce5-449">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-449">string</span></span>|<span data-ttu-id="dfce5-450">32 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-450">32 characters</span></span>|<span data-ttu-id="dfce5-451">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-451">✔</span></span>|<span data-ttu-id="dfce5-452">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="dfce5-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="dfce5-453">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-453">string</span></span>|<span data-ttu-id="dfce5-454">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-454">64 characters</span></span>||<span data-ttu-id="dfce5-455">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="dfce5-455">Type of the command.</span></span> <span data-ttu-id="dfce5-456">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="dfce5-456">One of `query` or `action`.</span></span> <span data-ttu-id="dfce5-457">Par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="dfce5-458">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-458">string</span></span>|<span data-ttu-id="dfce5-459">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-459">128 characters</span></span>||<span data-ttu-id="dfce5-460">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="dfce5-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="dfce5-461">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-461">boolean</span></span>|||<span data-ttu-id="dfce5-462">Une valeur booléle indique si la commande s’exécute initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="dfce5-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="dfce5-463">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="dfce5-464">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dfce5-464">array of Strings</span></span>|<span data-ttu-id="dfce5-465">3</span><span class="sxs-lookup"><span data-stu-id="dfce5-465">3</span></span>||<span data-ttu-id="dfce5-466">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="dfce5-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="dfce5-467">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="dfce5-468">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="dfce5-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="dfce5-469">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="dfce5-469">boolean</span></span>|||<span data-ttu-id="dfce5-470">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="dfce5-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="dfce5-471">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="dfce5-472">objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-472">object</span></span>|||<span data-ttu-id="dfce5-473">Spécifiez le module de tâche à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="dfce5-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="dfce5-474">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-474">string</span></span>|<span data-ttu-id="dfce5-475">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-475">64 characters</span></span>||<span data-ttu-id="dfce5-476">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="dfce5-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="dfce5-477">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-477">string</span></span>|||<span data-ttu-id="dfce5-478">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="dfce5-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="dfce5-479">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-479">string</span></span>|||<span data-ttu-id="dfce5-480">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » ou « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="dfce5-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="dfce5-481">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-481">string</span></span>|||<span data-ttu-id="dfce5-482">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="dfce5-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="dfce5-483">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-483">array of object</span></span>|<span data-ttu-id="dfce5-484">5 éléments</span><span class="sxs-lookup"><span data-stu-id="dfce5-484">5 items</span></span>|<span data-ttu-id="dfce5-485">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-485">✔</span></span>|<span data-ttu-id="dfce5-486">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="dfce5-486">The list of parameters the command takes.</span></span> <span data-ttu-id="dfce5-487">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="dfce5-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="dfce5-488">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-488">string</span></span>|<span data-ttu-id="dfce5-489">64 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-489">64 characters</span></span>|<span data-ttu-id="dfce5-490">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-490">✔</span></span>|<span data-ttu-id="dfce5-491">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="dfce5-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="dfce5-492">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="dfce5-493">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-493">string</span></span>|<span data-ttu-id="dfce5-494">32 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-494">32 characters</span></span>|<span data-ttu-id="dfce5-495">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-495">✔</span></span>|<span data-ttu-id="dfce5-496">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="dfce5-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="dfce5-497">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-497">string</span></span>|<span data-ttu-id="dfce5-498">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-498">128 characters</span></span>||<span data-ttu-id="dfce5-499">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="dfce5-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="dfce5-500">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-500">string</span></span>|<span data-ttu-id="dfce5-501">512 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-501">512 characters</span></span>||<span data-ttu-id="dfce5-502">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="dfce5-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="dfce5-503">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-503">string</span></span>|<span data-ttu-id="dfce5-504">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-504">128 characters</span></span>||<span data-ttu-id="dfce5-505">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="dfce5-506">L’un `text, textarea, number, date, time, toggle, choiceset` des .</span><span class="sxs-lookup"><span data-stu-id="dfce5-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="dfce5-507">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-507">array of objects</span></span>|<span data-ttu-id="dfce5-508">10 éléments</span><span class="sxs-lookup"><span data-stu-id="dfce5-508">10 items</span></span>||<span data-ttu-id="dfce5-509">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="dfce5-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="dfce5-510">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="dfce5-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="dfce5-511">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-511">string</span></span>|<span data-ttu-id="dfce5-512">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-512">128 characters</span></span>|<span data-ttu-id="dfce5-513">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-513">✔</span></span>|<span data-ttu-id="dfce5-514">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="dfce5-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="dfce5-515">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-515">string</span></span>|<span data-ttu-id="dfce5-516">512 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-516">512 characters</span></span>|<span data-ttu-id="dfce5-517">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-517">✔</span></span>|<span data-ttu-id="dfce5-518">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="dfce5-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="dfce5-519">autorisations</span><span class="sxs-lookup"><span data-stu-id="dfce5-519">permissions</span></span>

<span data-ttu-id="dfce5-520">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dfce5-520">**Optional** — array of strings</span></span>

<span data-ttu-id="dfce5-521">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir `string` comment fonctionne l’extension.</span><span class="sxs-lookup"><span data-stu-id="dfce5-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="dfce5-522">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="dfce5-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="dfce5-523">`identity`&emsp;Nécessite des informations d’identité d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="dfce5-524">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="dfce5-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="dfce5-525">Si vous modifiez ces autorisations pendant la mise à jour de l’application, vos utilisateurs répètent le processus de consentement après avoir exécuté l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="dfce5-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="dfce5-526">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) Mise à jour de votre application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="dfce5-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="dfce5-527">devicePermissions</span></span>

<span data-ttu-id="dfce5-528">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dfce5-528">**Optional** — array of strings</span></span>

<span data-ttu-id="dfce5-529">Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès.</span><span class="sxs-lookup"><span data-stu-id="dfce5-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="dfce5-530">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="dfce5-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="dfce5-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="dfce5-531">validDomains</span></span>

<span data-ttu-id="dfce5-532">**Facultatif,** sauf **obligatoire** lorsqu’il est indiqué.</span><span class="sxs-lookup"><span data-stu-id="dfce5-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="dfce5-533">Liste des domaines valides pour les sites web que l’application s’attend à charger dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="dfce5-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="dfce5-534">Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="dfce5-535">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="dfce5-536">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="dfce5-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="dfce5-537">Il **n’est** pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="dfce5-538">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="dfce5-539">Teams applications qui nécessitent leurs propres URL sharepoint pour fonctionner bien, inclut « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="dfce5-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfce5-540">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="dfce5-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="dfce5-541">Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="dfce5-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="dfce5-542">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="dfce5-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="dfce5-543">webApplicationInfo</span></span>

<span data-ttu-id="dfce5-544">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-544">**Optional** — object</span></span>

<span data-ttu-id="dfce5-545">Fournissez votre ID Azure Active Directory application (AAD) et des informations microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="dfce5-546">Si votre application est inscrite dans AAD, vous devez fournir l’ID de l’application, afin que les administrateurs peuvent facilement passer en revue les autorisations et accorder leur consentement dans Teams centre d’administration.</span><span class="sxs-lookup"><span data-stu-id="dfce5-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="dfce5-547">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-547">Name</span></span>| <span data-ttu-id="dfce5-548">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-548">Type</span></span>| <span data-ttu-id="dfce5-549">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-549">Maximum size</span></span> | <span data-ttu-id="dfce5-550">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-550">Required</span></span> | <span data-ttu-id="dfce5-551">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="dfce5-552">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-552">string</span></span>|<span data-ttu-id="dfce5-553">36 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-553">36 characters</span></span>|<span data-ttu-id="dfce5-554">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-554">✔</span></span>|<span data-ttu-id="dfce5-555">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-555">AAD application id of the app.</span></span> <span data-ttu-id="dfce5-556">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="dfce5-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="dfce5-557">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-557">string</span></span>|<span data-ttu-id="dfce5-558">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-558">2048 characters</span></span>|<span data-ttu-id="dfce5-559">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-559">✔</span></span>|<span data-ttu-id="dfce5-560">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="dfce5-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="dfce5-561">**REMARQUE :** Si vous n’utilisez pas l' sso, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, pour éviter une réponse https://notapplicable d’erreur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="dfce5-562">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dfce5-562">array of strings</span></span>|<span data-ttu-id="dfce5-563">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-563">128 characters</span></span>||<span data-ttu-id="dfce5-564">Spécifiez le consentement précis [spécifique à une ressource.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="dfce5-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="dfce5-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="dfce5-565">showLoadingIndicator</span></span>

<span data-ttu-id="dfce5-566">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="dfce5-566">**Optional** — boolean</span></span>

<span data-ttu-id="dfce5-567">Indique si l’indicateur de chargement s’affiche ou non lorsqu’une application ou un onglet est en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="dfce5-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="dfce5-568">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="dfce5-569">Si vous sélectionnez true dans le manifeste de votre application, pour charger la page correctement, modifiez les pages de contenu de vos onglets et modules de tâche comme décrit dans Afficher un document d’indicateur de chargement `showLoadingIndicator` natif. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="dfce5-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="dfce5-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="dfce5-570">isFullScreen</span></span>

 <span data-ttu-id="dfce5-571">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="dfce5-571">**Optional** — boolean</span></span>

<span data-ttu-id="dfce5-572">Indiquez l’endroit où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="dfce5-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="dfce5-573">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="dfce5-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="dfce5-574">activités</span><span class="sxs-lookup"><span data-stu-id="dfce5-574">activities</span></span>

<span data-ttu-id="dfce5-575">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-575">**Optional** — object</span></span>

<span data-ttu-id="dfce5-576">Définissez les propriétés que votre application utilise pour publier un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="dfce5-577">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-577">Name</span></span>| <span data-ttu-id="dfce5-578">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-578">Type</span></span>| <span data-ttu-id="dfce5-579">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-579">Maximum size</span></span> | <span data-ttu-id="dfce5-580">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-580">Required</span></span> | <span data-ttu-id="dfce5-581">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="dfce5-582">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="dfce5-582">array of Objects</span></span>|<span data-ttu-id="dfce5-583">128 éléments</span><span class="sxs-lookup"><span data-stu-id="dfce5-583">128 items</span></span>| | <span data-ttu-id="dfce5-584">Fournissez les types d’activités que votre application peut publier dans un flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dfce5-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="dfce5-585">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="dfce5-585">activities.activityTypes</span></span>

|<span data-ttu-id="dfce5-586">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-586">Name</span></span>| <span data-ttu-id="dfce5-587">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-587">Type</span></span>| <span data-ttu-id="dfce5-588">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-588">Maximum size</span></span> | <span data-ttu-id="dfce5-589">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-589">Required</span></span> | <span data-ttu-id="dfce5-590">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="dfce5-591">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-591">string</span></span>|<span data-ttu-id="dfce5-592">32 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-592">32 characters</span></span>|<span data-ttu-id="dfce5-593">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-593">✔</span></span>|<span data-ttu-id="dfce5-594">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="dfce5-594">The notification type.</span></span> <span data-ttu-id="dfce5-595">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="dfce5-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="dfce5-596">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-596">string</span></span>|<span data-ttu-id="dfce5-597">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-597">128 characters</span></span>|<span data-ttu-id="dfce5-598">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-598">✔</span></span>|<span data-ttu-id="dfce5-599">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="dfce5-599">A brief description of the notification.</span></span> <span data-ttu-id="dfce5-600">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="dfce5-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="dfce5-601">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-601">string</span></span>|<span data-ttu-id="dfce5-602">128 caractères</span><span class="sxs-lookup"><span data-stu-id="dfce5-602">128 characters</span></span>|<span data-ttu-id="dfce5-603">✔</span><span class="sxs-lookup"><span data-stu-id="dfce5-603">✔</span></span>|<span data-ttu-id="dfce5-604">Ex: « {actor} created task {taskId} for you »</span><span class="sxs-lookup"><span data-stu-id="dfce5-604">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="dfce5-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="dfce5-605">defaultInstallScope</span></span>

<span data-ttu-id="dfce5-606">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="dfce5-606">**Optional** - string</span></span>

<span data-ttu-id="dfce5-607">Spécifie l’étendue d’installation définie par défaut pour cette application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="dfce5-608">L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="dfce5-609">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="dfce5-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="dfce5-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="dfce5-610">defaultGroupCapability</span></span>

<span data-ttu-id="dfce5-611">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="dfce5-611">**Optional** - object</span></span>

<span data-ttu-id="dfce5-612">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="dfce5-613">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="dfce5-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="dfce5-614">Nom</span><span class="sxs-lookup"><span data-stu-id="dfce5-614">Name</span></span>| <span data-ttu-id="dfce5-615">Type</span><span class="sxs-lookup"><span data-stu-id="dfce5-615">Type</span></span>| <span data-ttu-id="dfce5-616">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="dfce5-616">Maximum size</span></span> | <span data-ttu-id="dfce5-617">Requis</span><span class="sxs-lookup"><span data-stu-id="dfce5-617">Required</span></span> | <span data-ttu-id="dfce5-618">Description</span><span class="sxs-lookup"><span data-stu-id="dfce5-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="dfce5-619">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-619">string</span></span>|||<span data-ttu-id="dfce5-620">Lorsque l’étendue d’installation sélectionnée `team` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="dfce5-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="dfce5-621">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="dfce5-622">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-622">string</span></span>|||<span data-ttu-id="dfce5-623">Lorsque l’étendue d’installation sélectionnée `groupchat` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="dfce5-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="dfce5-624">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="dfce5-625">string</span><span class="sxs-lookup"><span data-stu-id="dfce5-625">string</span></span>|||<span data-ttu-id="dfce5-626">Lorsque l’étendue d’installation sélectionnée `meetings` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="dfce5-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="dfce5-627">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="dfce5-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="dfce5-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="dfce5-628">configurableProperties</span></span>

<span data-ttu-id="dfce5-629">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="dfce5-629">**Optional** - array</span></span>

<span data-ttu-id="dfce5-630">Le `configurableProperties` bloc définit les propriétés d’application que Teams administrateur peut personnaliser.</span><span class="sxs-lookup"><span data-stu-id="dfce5-630">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="dfce5-631">Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="dfce5-631">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="dfce5-632">Au moins une propriété doit être définie.</span><span class="sxs-lookup"><span data-stu-id="dfce5-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="dfce5-633">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="dfce5-633">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="dfce5-634">En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-634">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="dfce5-635">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfce5-635">You can define any of the following properties:</span></span>
* <span data-ttu-id="dfce5-636">`name`: permet à l’administrateur de modifier le nom complet de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-636">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="dfce5-637">`shortDescription`: permet à l’administrateur de modifier la description courte de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-637">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="dfce5-638">`longDescription`: permet à l’administrateur de modifier la description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfce5-638">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="dfce5-639">`smallImageUrl`: il s’agit `outline` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="dfce5-639">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="dfce5-640">`largeImageUrl`: il s’agit `color` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="dfce5-640">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="dfce5-641">`accentColor`: il s’agit de la couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="dfce5-641">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="dfce5-642">`websiteUrl`: il s’agit https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-642">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="dfce5-643">`privacyUrl`: il s’agit https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-643">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="dfce5-644">`termsOfUseUrl`: il s’agit de https:// URL des conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="dfce5-644">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


