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
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="b671e-104">Référence: Schéma manifeste pour les Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b671e-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="b671e-105">Le Teams décrit comment l’application s’intègre dans le Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="b671e-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="b671e-106">Votre manifeste doit se conformer au schéma hébergé à [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="b671e-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="b671e-107">Les versions précédentes 1.0, 1.1,..., 1.6, et ainsi de suite sont également prises en charge (en utilisant « v1.x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="b671e-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="b671e-108">L’échantillon de schéma suivant montre toutes les options d’extensibilité :</span><span class="sxs-lookup"><span data-stu-id="b671e-108">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="b671e-109">Exemple manifeste complet</span><span class="sxs-lookup"><span data-stu-id="b671e-109">Sample full manifest</span></span>

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

<span data-ttu-id="b671e-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b671e-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="b671e-111">$schema</span><span class="sxs-lookup"><span data-stu-id="b671e-111">$schema</span></span>

<span data-ttu-id="b671e-112">Facultatif, mais recommandé — chaîne</span><span class="sxs-lookup"><span data-stu-id="b671e-112">Optional, but recommended — string</span></span>

<span data-ttu-id="b671e-113">L https:// URL faisant référence au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="b671e-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="b671e-114">manifesteVersion</span><span class="sxs-lookup"><span data-stu-id="b671e-114">manifestVersion</span></span>

<span data-ttu-id="b671e-115">**Requis** — chaîne</span><span class="sxs-lookup"><span data-stu-id="b671e-115">**Required** — string</span></span>

<span data-ttu-id="b671e-116">La version du schéma manifeste que ce manifeste utilise.</span><span class="sxs-lookup"><span data-stu-id="b671e-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="b671e-117">Il doit être 1,10.</span><span class="sxs-lookup"><span data-stu-id="b671e-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="b671e-118">version</span><span class="sxs-lookup"><span data-stu-id="b671e-118">version</span></span>

<span data-ttu-id="b671e-119">**Requis** — chaîne</span><span class="sxs-lookup"><span data-stu-id="b671e-119">**Required** — string</span></span>

<span data-ttu-id="b671e-120">La version d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="b671e-120">The version of a specific app.</span></span> <span data-ttu-id="b671e-121">Si vous mettez à jour quelque chose dans votre manifeste, la version doit être incrémentée aussi.</span><span class="sxs-lookup"><span data-stu-id="b671e-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="b671e-122">De cette façon, lorsque le nouveau manifeste est installé, il l’réécrit et l’utilisateur reçoit la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b671e-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="b671e-123">Si cette application a été soumise au magasin, le nouveau manifeste doit être soumis à nouveau et re-validé.</span><span class="sxs-lookup"><span data-stu-id="b671e-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="b671e-124">Les utilisateurs de l’application reçoivent automatiquement le nouveau manifeste mis à jour dans les heures qui ont immédiatement après l’approbation du manifeste.</span><span class="sxs-lookup"><span data-stu-id="b671e-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="b671e-125">Si les demandes d’autorisations de l’application changent, les utilisateurs sont invités à mettre à niveau et à consentir à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="b671e-126">Cette chaîne de version doit suivre la [norme semver](http://semver.org/) (MAJOR. mineur. PATCH).</span><span class="sxs-lookup"><span data-stu-id="b671e-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="b671e-127">id</span><span class="sxs-lookup"><span data-stu-id="b671e-127">id</span></span>

<span data-ttu-id="b671e-128">**Requis** — Id d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="b671e-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="b671e-129">L’ID est un identifiant unique généré par Microsoft pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="b671e-130">Vous avez un IDENTIFIANT si votre bot est enregistré via le Microsoft Bot Framework ou l’application Web de votre onglet se signe déjà avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b671e-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="b671e-131">Vous devez entrer l’iD ici.</span><span class="sxs-lookup"><span data-stu-id="b671e-131">You must enter the ID here.</span></span> <span data-ttu-id="b671e-132">Sinon, vous devez générer un nouvel ID sur le portail [d’enregistrement des applications Microsoft](https://aka.ms/appregistrations).</span><span class="sxs-lookup"><span data-stu-id="b671e-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="b671e-133">Utilisez le même ID si vous ajoutez un bot.</span><span class="sxs-lookup"><span data-stu-id="b671e-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="b671e-134">Si vous soumettez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="b671e-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="b671e-135">developer</span><span class="sxs-lookup"><span data-stu-id="b671e-135">developer</span></span>

<span data-ttu-id="b671e-136">**Requis** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-136">**Required** — object</span></span>

<span data-ttu-id="b671e-137">Spécifie les informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="b671e-137">Specifies information about your company.</span></span> <span data-ttu-id="b671e-138">Pour les applications soumises au magasin Teams, ces valeurs doivent correspondre aux informations contenues dans votre annonce de magasin.</span><span class="sxs-lookup"><span data-stu-id="b671e-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="b671e-139">Pour plus d’informations, consultez les lignes [directrices Teams’édition en magasin.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="b671e-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="b671e-140">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-140">Name</span></span>| <span data-ttu-id="b671e-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-141">Maximum size</span></span> | <span data-ttu-id="b671e-142">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-142">Required</span></span> | <span data-ttu-id="b671e-143">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="b671e-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-144">32 characters</span></span>|<span data-ttu-id="b671e-145">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-145">✔</span></span>|<span data-ttu-id="b671e-146">Le nom d’affichage du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="b671e-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-147">2048 characters</span></span>|<span data-ttu-id="b671e-148">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-148">✔</span></span>|<span data-ttu-id="b671e-149">L https:// URL du site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="b671e-150">Ce lien doit emmener les utilisateurs vers votre entreprise ou votre page de destination spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="b671e-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="b671e-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-151">2048 characters</span></span>|<span data-ttu-id="b671e-152">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-152">✔</span></span>|<span data-ttu-id="b671e-153">Le https:// URL de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="b671e-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-154">2048 characters</span></span>|<span data-ttu-id="b671e-155">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-155">✔</span></span>|<span data-ttu-id="b671e-156">Le https:// URL aux conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="b671e-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-157">10 characters</span></span>| |<span data-ttu-id="b671e-158">**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="b671e-159">name</span><span class="sxs-lookup"><span data-stu-id="b671e-159">name</span></span>

<span data-ttu-id="b671e-160">**Requis** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-160">**Required** — object</span></span>

<span data-ttu-id="b671e-161">Le nom de votre expérience d’application, affiché aux utilisateurs dans l’expérience Teams’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="b671e-162">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="b671e-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="b671e-163">Les valeurs et `short` doivent `full` être différentes.</span><span class="sxs-lookup"><span data-stu-id="b671e-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="b671e-164">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-164">Name</span></span>| <span data-ttu-id="b671e-165">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-165">Maximum size</span></span> | <span data-ttu-id="b671e-166">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-166">Required</span></span> | <span data-ttu-id="b671e-167">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b671e-168">30 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-168">30 characters</span></span>|<span data-ttu-id="b671e-169">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-169">✔</span></span>|<span data-ttu-id="b671e-170">Le nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="b671e-171">100 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-171">100 characters</span></span>||<span data-ttu-id="b671e-172">Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="b671e-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="b671e-173">description</span><span class="sxs-lookup"><span data-stu-id="b671e-173">description</span></span>

<span data-ttu-id="b671e-174">**Requis** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-174">**Required** — object</span></span>

<span data-ttu-id="b671e-175">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b671e-175">Describes your app to users.</span></span> <span data-ttu-id="b671e-176">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="b671e-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="b671e-177">Assurez-vous que votre description décrit avec précision votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="b671e-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="b671e-178">Vous devez noter dans la description complète, si un compte externe est nécessaire pour une utilisation.</span><span class="sxs-lookup"><span data-stu-id="b671e-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="b671e-179">Les valeurs et `short` doivent `full` être différentes.</span><span class="sxs-lookup"><span data-stu-id="b671e-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="b671e-180">Votre courte description ne doit pas être répétée dans la longue description et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="b671e-181">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-181">Name</span></span>| <span data-ttu-id="b671e-182">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-182">Maximum size</span></span> | <span data-ttu-id="b671e-183">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-183">Required</span></span> | <span data-ttu-id="b671e-184">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b671e-185">80 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-185">80 characters</span></span>|<span data-ttu-id="b671e-186">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-186">✔</span></span>|<span data-ttu-id="b671e-187">Une courte description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="b671e-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="b671e-188">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-188">4000 characters</span></span>|<span data-ttu-id="b671e-189">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-189">✔</span></span>|<span data-ttu-id="b671e-190">La description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="b671e-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="b671e-191">packageName PackageName PackageName packageName</span><span class="sxs-lookup"><span data-stu-id="b671e-191">packageName</span></span>

<span data-ttu-id="b671e-192">**Facultatif** — chaîne</span><span class="sxs-lookup"><span data-stu-id="b671e-192">**Optional** — string</span></span>

<span data-ttu-id="b671e-193">Un identificateur unique pour l’application dans la notation de domaine inversé; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="b671e-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="b671e-194">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="b671e-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="b671e-195">localisationInfo</span><span class="sxs-lookup"><span data-stu-id="b671e-195">localizationInfo</span></span>

<span data-ttu-id="b671e-196">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-196">**Optional** — object</span></span>

<span data-ttu-id="b671e-197">Permet la spécification d’une langue par défaut, ainsi que des pointeurs à des fichiers linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b671e-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="b671e-198">Pour plus d’informations, [voir localisation](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="b671e-198">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="b671e-199">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-199">Name</span></span>| <span data-ttu-id="b671e-200">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-200">Maximum size</span></span> | <span data-ttu-id="b671e-201">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-201">Required</span></span> | <span data-ttu-id="b671e-202">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="b671e-203">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-203">✔</span></span>|<span data-ttu-id="b671e-204">L’étiquette de langue des chaînes dans ce fichier manifeste de haut niveau.</span><span class="sxs-lookup"><span data-stu-id="b671e-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="b671e-205">localisationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="b671e-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="b671e-206">Un éventail d’objets spécifier des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b671e-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="b671e-207">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-207">Name</span></span>| <span data-ttu-id="b671e-208">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-208">Maximum size</span></span> | <span data-ttu-id="b671e-209">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-209">Required</span></span> | <span data-ttu-id="b671e-210">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="b671e-211">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-211">✔</span></span>|<span data-ttu-id="b671e-212">L’étiquette linguistique des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="b671e-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="b671e-213">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-213">✔</span></span>|<span data-ttu-id="b671e-214">Un chemin de fichier relatif vers un fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="b671e-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="b671e-215">icons</span><span class="sxs-lookup"><span data-stu-id="b671e-215">icons</span></span>

<span data-ttu-id="b671e-216">**Requis** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-216">**Required** — object</span></span>

<span data-ttu-id="b671e-217">Icônes utilisées dans l’application Teams’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-217">Icons used within the Teams app.</span></span> <span data-ttu-id="b671e-218">Les fichiers icônes doivent être inclus dans le paquet de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="b671e-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="b671e-219">Voir [Icônes pour](../../concepts/build-and-test/apps-package.md#app-icons) plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b671e-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="b671e-220">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-220">Name</span></span>| <span data-ttu-id="b671e-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-221">Maximum size</span></span> | <span data-ttu-id="b671e-222">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-222">Required</span></span> | <span data-ttu-id="b671e-223">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="b671e-224">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="b671e-224">32 x 32 pixels</span></span>|<span data-ttu-id="b671e-225">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-225">✔</span></span>|<span data-ttu-id="b671e-226">Un chemin de fichier relatif vers une icône transparente de contour PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="b671e-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="b671e-227">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="b671e-227">192 x 192 pixels</span></span>|<span data-ttu-id="b671e-228">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-228">✔</span></span>|<span data-ttu-id="b671e-229">Un chemin de fichier relatif vers une icône PNG 192x192 en couleur.</span><span class="sxs-lookup"><span data-stu-id="b671e-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="b671e-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="b671e-230">accentColor</span></span>

<span data-ttu-id="b671e-231">**Facultatif** — Code couleur HTML Hex</span><span class="sxs-lookup"><span data-stu-id="b671e-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="b671e-232">Une couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.</span><span class="sxs-lookup"><span data-stu-id="b671e-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="b671e-233">La valeur doit être un code couleur HTML valide commençant par '#', par exemple `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="b671e-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="b671e-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="b671e-234">configurableTabs</span></span>

<span data-ttu-id="b671e-235">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-235">**Optional** — array</span></span>

<span data-ttu-id="b671e-236">Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="b671e-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="b671e-237">Les onglets configurables ne sont pris en charge que dans la portée des équipes et vous pouvez configurer les mêmes onglets plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="b671e-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="b671e-238">Toutefois, vous ne pouvez le définir dans le manifeste qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="b671e-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="b671e-239">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-239">Name</span></span>| <span data-ttu-id="b671e-240">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-240">Type</span></span>| <span data-ttu-id="b671e-241">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-241">Maximum size</span></span> | <span data-ttu-id="b671e-242">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-242">Required</span></span> | <span data-ttu-id="b671e-243">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b671e-244">string</span><span class="sxs-lookup"><span data-stu-id="b671e-244">string</span></span>|<span data-ttu-id="b671e-245">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-245">2048 characters</span></span>|<span data-ttu-id="b671e-246">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-246">✔</span></span>|<span data-ttu-id="b671e-247">L https:// URL à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="b671e-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="b671e-248">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-248">array of enums</span></span>|<span data-ttu-id="b671e-249">1</span><span class="sxs-lookup"><span data-stu-id="b671e-249">1</span></span>|<span data-ttu-id="b671e-250">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-250">✔</span></span>|<span data-ttu-id="b671e-251">Actuellement, les onglets configurables ne supportent que `team` les `groupchat` étendues et les étendues.</span><span class="sxs-lookup"><span data-stu-id="b671e-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="b671e-252">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-252">boolean</span></span>|||<span data-ttu-id="b671e-253">Une valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après la création.</span><span class="sxs-lookup"><span data-stu-id="b671e-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="b671e-254">Par défaut: **vrai**.</span><span class="sxs-lookup"><span data-stu-id="b671e-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="b671e-255">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-255">array of enums</span></span>|<span data-ttu-id="b671e-256">6 </span><span class="sxs-lookup"><span data-stu-id="b671e-256">6</span></span>||<span data-ttu-id="b671e-257">L’ensemble des `contextItem` étendues où un [onglet est pris en charge](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="b671e-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="b671e-258">Par défaut: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="b671e-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="b671e-259">string</span><span class="sxs-lookup"><span data-stu-id="b671e-259">string</span></span>|<span data-ttu-id="b671e-260">2048</span><span class="sxs-lookup"><span data-stu-id="b671e-260">2048</span></span>||<span data-ttu-id="b671e-261">Un chemin de fichier relatif vers une image d’aperçu d’onglet pour une utilisation SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b671e-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="b671e-262">Taille 1024x768.</span><span class="sxs-lookup"><span data-stu-id="b671e-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="b671e-263">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-263">array of enums</span></span>|<span data-ttu-id="b671e-264">1</span><span class="sxs-lookup"><span data-stu-id="b671e-264">1</span></span>||<span data-ttu-id="b671e-265">Définit la façon dont votre onglet est disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b671e-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="b671e-266">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="b671e-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="b671e-267">staticTabs StaticTabs StaticTabs staticTab</span><span class="sxs-lookup"><span data-stu-id="b671e-267">staticTabs</span></span>

<span data-ttu-id="b671e-268">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-268">**Optional** — array</span></span>

<span data-ttu-id="b671e-269">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="b671e-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="b671e-270">Les onglets statiques déclarés `personal` dans la portée sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="b671e-271">Les onglets statiques déclarés dans la `team` portée ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b671e-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="b671e-272">Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du `object` type.</span><span class="sxs-lookup"><span data-stu-id="b671e-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="b671e-273">Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="b671e-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="b671e-274">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-274">Name</span></span>| <span data-ttu-id="b671e-275">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-275">Type</span></span>| <span data-ttu-id="b671e-276">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-276">Maximum size</span></span> | <span data-ttu-id="b671e-277">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-277">Required</span></span> | <span data-ttu-id="b671e-278">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="b671e-279">string</span><span class="sxs-lookup"><span data-stu-id="b671e-279">string</span></span>|<span data-ttu-id="b671e-280">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-280">64 characters</span></span>|<span data-ttu-id="b671e-281">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-281">✔</span></span>|<span data-ttu-id="b671e-282">Un identificateur unique pour l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="b671e-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="b671e-283">string</span><span class="sxs-lookup"><span data-stu-id="b671e-283">string</span></span>|<span data-ttu-id="b671e-284">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-284">128 characters</span></span>|<span data-ttu-id="b671e-285">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-285">✔</span></span>|<span data-ttu-id="b671e-286">Le nom d’affichage de l’onglet dans l’interface du canal.</span><span class="sxs-lookup"><span data-stu-id="b671e-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="b671e-287">string</span><span class="sxs-lookup"><span data-stu-id="b671e-287">string</span></span>||<span data-ttu-id="b671e-288">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-288">✔</span></span>|<span data-ttu-id="b671e-289">L https:// URL qui indique l’interface utilisateur de l’entité à afficher dans la Teams externe.</span><span class="sxs-lookup"><span data-stu-id="b671e-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="b671e-290">string</span><span class="sxs-lookup"><span data-stu-id="b671e-290">string</span></span>|||<span data-ttu-id="b671e-291">L https:// URL à pointer vers si un utilisateur choisit de voir dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="b671e-292">string</span><span class="sxs-lookup"><span data-stu-id="b671e-292">string</span></span>|||<span data-ttu-id="b671e-293">L https:// URL à pointer vers les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="b671e-294">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-294">array of enums</span></span>|<span data-ttu-id="b671e-295">1</span><span class="sxs-lookup"><span data-stu-id="b671e-295">1</span></span>|<span data-ttu-id="b671e-296">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-296">✔</span></span>|<span data-ttu-id="b671e-297">Actuellement, les onglets statiques ne supportent que `personal` la portée, ce qui signifie qu’il ne peut être provisionné que dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="b671e-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="b671e-298">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-298">array of enums</span></span>| <span data-ttu-id="b671e-299">2</span><span class="sxs-lookup"><span data-stu-id="b671e-299">2</span></span>|| <span data-ttu-id="b671e-300">L’ensemble des `contextItem` étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b671e-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="b671e-301">La fonctionnalité searchUrl n’est pas disponible pour les développeurs tiers.</span><span class="sxs-lookup"><span data-stu-id="b671e-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="b671e-302">Si vos onglets nécessitent des informations dépendantes du contexte pour afficher le contenu pertinent ou pour lancer un flux d’authentification, Pour plus d’informations, [consultez Le contexte de votre Microsoft Teams onglet](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="b671e-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="b671e-303">Bots</span><span class="sxs-lookup"><span data-stu-id="b671e-303">bots</span></span>

<span data-ttu-id="b671e-304">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-304">**Optional** — array</span></span>

<span data-ttu-id="b671e-305">Définit une solution bot, ainsi que des informations optionnelles telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="b671e-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="b671e-306">L’élément est un tableau (maximum de seulement 1 élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="b671e-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="b671e-307">Ce bloc n’est nécessaire que pour les solutions qui fournissent une expérience bot.</span><span class="sxs-lookup"><span data-stu-id="b671e-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="b671e-308">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-308">Name</span></span>| <span data-ttu-id="b671e-309">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-309">Type</span></span>| <span data-ttu-id="b671e-310">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-310">Maximum size</span></span> | <span data-ttu-id="b671e-311">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-311">Required</span></span> | <span data-ttu-id="b671e-312">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b671e-313">string</span><span class="sxs-lookup"><span data-stu-id="b671e-313">string</span></span>|<span data-ttu-id="b671e-314">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-314">64 characters</span></span>|<span data-ttu-id="b671e-315">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-315">✔</span></span>|<span data-ttu-id="b671e-316">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b671e-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="b671e-317">Cela peut bien être le même que l’ID de [l’application globale](#id).</span><span class="sxs-lookup"><span data-stu-id="b671e-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="b671e-318">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-318">array of enums</span></span>|<span data-ttu-id="b671e-319">3</span><span class="sxs-lookup"><span data-stu-id="b671e-319">3</span></span>|<span data-ttu-id="b671e-320">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-320">✔</span></span>|<span data-ttu-id="b671e-321">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="b671e-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b671e-322">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="b671e-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="b671e-323">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-323">boolean</span></span>|||<span data-ttu-id="b671e-324">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="b671e-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="b671e-325">faire défaut: **`false`**</span><span class="sxs-lookup"><span data-stu-id="b671e-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="b671e-326">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-326">boolean</span></span>|||<span data-ttu-id="b671e-327">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="b671e-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="b671e-328">faire défaut: **`false`**</span><span class="sxs-lookup"><span data-stu-id="b671e-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="b671e-329">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-329">boolean</span></span>|||<span data-ttu-id="b671e-330">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="b671e-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="b671e-331">faire défaut: **`false`**</span><span class="sxs-lookup"><span data-stu-id="b671e-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="b671e-332">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-332">boolean</span></span>|||<span data-ttu-id="b671e-333">Une valeur indiquant où un bot prend en charge l’appel audio.</span><span class="sxs-lookup"><span data-stu-id="b671e-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="b671e-334">**IMPORTANT**: Cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="b671e-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="b671e-335">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des changements avant d’être pleinement disponibles.</span><span class="sxs-lookup"><span data-stu-id="b671e-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="b671e-336">Il n’est fourni qu’à des fins d’essai et d’exploration et ne doit pas être utilisé dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="b671e-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="b671e-337">faire défaut: **`false`**</span><span class="sxs-lookup"><span data-stu-id="b671e-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="b671e-338">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-338">boolean</span></span>|||<span data-ttu-id="b671e-339">Une valeur indiquant où un bot prend en charge l’appel vidéo.</span><span class="sxs-lookup"><span data-stu-id="b671e-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="b671e-340">**IMPORTANT**: Cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="b671e-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="b671e-341">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des changements avant d’être pleinement disponibles.</span><span class="sxs-lookup"><span data-stu-id="b671e-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="b671e-342">Il n’est fourni qu’à des fins d’essai et d’exploration et ne doit pas être utilisé dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="b671e-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="b671e-343">faire défaut: **`false`**</span><span class="sxs-lookup"><span data-stu-id="b671e-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="b671e-344">bots.commandLists (en)</span><span class="sxs-lookup"><span data-stu-id="b671e-344">bots.commandLists</span></span>

<span data-ttu-id="b671e-345">Une liste optionnelle de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b671e-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="b671e-346">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commande distincte pour chaque champ d’application que votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="b671e-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="b671e-347">Consultez les [menus Bot pour](~/bots/how-to/create-a-bot-commands-menu.md) plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b671e-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="b671e-348">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-348">Name</span></span>| <span data-ttu-id="b671e-349">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-349">Type</span></span>| <span data-ttu-id="b671e-350">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-350">Maximum size</span></span> | <span data-ttu-id="b671e-351">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-351">Required</span></span> | <span data-ttu-id="b671e-352">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="b671e-353">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-353">array of enums</span></span>|<span data-ttu-id="b671e-354">3</span><span class="sxs-lookup"><span data-stu-id="b671e-354">3</span></span>|<span data-ttu-id="b671e-355">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-355">✔</span></span>|<span data-ttu-id="b671e-356">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="b671e-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="b671e-357">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="b671e-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="b671e-358">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-358">array of objects</span></span>|<span data-ttu-id="b671e-359">10</span><span class="sxs-lookup"><span data-stu-id="b671e-359">10</span></span>|<span data-ttu-id="b671e-360">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-360">✔</span></span>|<span data-ttu-id="b671e-361">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="b671e-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="b671e-362">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="b671e-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="b671e-363">`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).</span><span class="sxs-lookup"><span data-stu-id="b671e-363">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="b671e-364">bots.commandLists.commands (en)</span><span class="sxs-lookup"><span data-stu-id="b671e-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="b671e-365">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-365">Name</span></span>| <span data-ttu-id="b671e-366">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-366">Type</span></span>| <span data-ttu-id="b671e-367">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-367">Maximum size</span></span> | <span data-ttu-id="b671e-368">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-368">Required</span></span> | <span data-ttu-id="b671e-369">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="b671e-370">title</span><span class="sxs-lookup"><span data-stu-id="b671e-370">title</span></span>|<span data-ttu-id="b671e-371">string</span><span class="sxs-lookup"><span data-stu-id="b671e-371">string</span></span>|<span data-ttu-id="b671e-372">12 </span><span class="sxs-lookup"><span data-stu-id="b671e-372">12</span></span>|<span data-ttu-id="b671e-373">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-373">✔</span></span>|<span data-ttu-id="b671e-374">Le nom de commande bot.</span><span class="sxs-lookup"><span data-stu-id="b671e-374">The bot command name.</span></span>|
|<span data-ttu-id="b671e-375">description</span><span class="sxs-lookup"><span data-stu-id="b671e-375">description</span></span>|<span data-ttu-id="b671e-376">string</span><span class="sxs-lookup"><span data-stu-id="b671e-376">string</span></span>|<span data-ttu-id="b671e-377">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-377">128 characters</span></span>|<span data-ttu-id="b671e-378">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-378">✔</span></span>|<span data-ttu-id="b671e-379">Une simple description de texte ou un exemple de la syntaxe de commande et de ses arguments.</span><span class="sxs-lookup"><span data-stu-id="b671e-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="b671e-380">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b671e-380">connectors</span></span>

<span data-ttu-id="b671e-381">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-381">**Optional** — array</span></span>

<span data-ttu-id="b671e-382">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="b671e-383">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="b671e-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b671e-384">Ce bloc n’est nécessaire que pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="b671e-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="b671e-385">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-385">Name</span></span>| <span data-ttu-id="b671e-386">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-386">Type</span></span>| <span data-ttu-id="b671e-387">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-387">Maximum size</span></span> | <span data-ttu-id="b671e-388">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-388">Required</span></span> | <span data-ttu-id="b671e-389">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b671e-390">string</span><span class="sxs-lookup"><span data-stu-id="b671e-390">string</span></span>|<span data-ttu-id="b671e-391">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-391">2048 characters</span></span>|<span data-ttu-id="b671e-392">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-392">✔</span></span>|<span data-ttu-id="b671e-393">L https:// URL à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="b671e-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="b671e-394">tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b671e-394">array of enums</span></span>|<span data-ttu-id="b671e-395">1</span><span class="sxs-lookup"><span data-stu-id="b671e-395">1</span></span>|<span data-ttu-id="b671e-396">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-396">✔</span></span>|<span data-ttu-id="b671e-397">Précise si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="b671e-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b671e-398">Actuellement, seule la portée `team` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b671e-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="b671e-399">string</span><span class="sxs-lookup"><span data-stu-id="b671e-399">string</span></span>|<span data-ttu-id="b671e-400">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-400">64 characters</span></span>|<span data-ttu-id="b671e-401">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-401">✔</span></span>|<span data-ttu-id="b671e-402">Un identificateur unique pour le connecteur qui correspond à son ID dans le tableau de [bord des développeurs de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="b671e-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="b671e-403">composerExtensions</span><span class="sxs-lookup"><span data-stu-id="b671e-403">composeExtensions</span></span>

<span data-ttu-id="b671e-404">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-404">**Optional** — array</span></span>

<span data-ttu-id="b671e-405">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="b671e-406">Le nom de la fonctionnalité a été changé de « composer extension » à « extension de messagerie » en Novembre 2017, mais le nom manifeste reste le même de sorte que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="b671e-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="b671e-407">L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="b671e-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b671e-408">Ce bloc n’est nécessaire que pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="b671e-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="b671e-409">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-409">Name</span></span>| <span data-ttu-id="b671e-410">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-410">Type</span></span> | <span data-ttu-id="b671e-411">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-411">Maximum Size</span></span> | <span data-ttu-id="b671e-412">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="b671e-412">Required</span></span> | <span data-ttu-id="b671e-413">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b671e-414">string</span><span class="sxs-lookup"><span data-stu-id="b671e-414">string</span></span>|<span data-ttu-id="b671e-415">64</span><span class="sxs-lookup"><span data-stu-id="b671e-415">64</span></span>|<span data-ttu-id="b671e-416">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-416">✔</span></span>|<span data-ttu-id="b671e-417">L’iD unique de l’application Microsoft pour le bot qui prend en arrière l’extension de messagerie, tel qu’enregistré avec le Cadre Bot.</span><span class="sxs-lookup"><span data-stu-id="b671e-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="b671e-418">Cela peut bien être le même que l’ID app globale.</span><span class="sxs-lookup"><span data-stu-id="b671e-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="b671e-419">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-419">array of objects</span></span>|<span data-ttu-id="b671e-420">10</span><span class="sxs-lookup"><span data-stu-id="b671e-420">10</span></span>|<span data-ttu-id="b671e-421">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-421">✔</span></span>|<span data-ttu-id="b671e-422">Tableau de commandes pris en charge par l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="b671e-422">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="b671e-423">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-423">boolean</span></span>|||<span data-ttu-id="b671e-424">Une valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="b671e-425">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b671e-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="b671e-426">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-426">array of Objects</span></span>|<span data-ttu-id="b671e-427">5 </span><span class="sxs-lookup"><span data-stu-id="b671e-427">5</span></span>||<span data-ttu-id="b671e-428">Une liste de gestionnaires qui permettent d’invoquer les applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="b671e-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="b671e-429">string</span><span class="sxs-lookup"><span data-stu-id="b671e-429">string</span></span>|||<span data-ttu-id="b671e-430">Le type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="b671e-430">The type of message handler.</span></span> <span data-ttu-id="b671e-431">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="b671e-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="b671e-432">tableau de cordes</span><span class="sxs-lookup"><span data-stu-id="b671e-432">array of Strings</span></span>|||<span data-ttu-id="b671e-433">Tableau des domaines pour qui le gestionnaire de message de lien peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="b671e-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="b671e-434">composerExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="b671e-434">composeExtensions.commands</span></span>

<span data-ttu-id="b671e-435">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="b671e-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="b671e-436">Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="b671e-437">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="b671e-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="b671e-438">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="b671e-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="b671e-439">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-439">Name</span></span>| <span data-ttu-id="b671e-440">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-440">Type</span></span>| <span data-ttu-id="b671e-441">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-441">Maximum size</span></span> | <span data-ttu-id="b671e-442">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-442">Required</span></span> | <span data-ttu-id="b671e-443">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b671e-444">string</span><span class="sxs-lookup"><span data-stu-id="b671e-444">string</span></span>|<span data-ttu-id="b671e-445">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-445">64 characters</span></span>|<span data-ttu-id="b671e-446">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-446">✔</span></span>|<span data-ttu-id="b671e-447">L’identification de la commande.</span><span class="sxs-lookup"><span data-stu-id="b671e-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="b671e-448">string</span><span class="sxs-lookup"><span data-stu-id="b671e-448">string</span></span>|<span data-ttu-id="b671e-449">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-449">32 characters</span></span>|<span data-ttu-id="b671e-450">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-450">✔</span></span>|<span data-ttu-id="b671e-451">Le nom de commande convivial.</span><span class="sxs-lookup"><span data-stu-id="b671e-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="b671e-452">string</span><span class="sxs-lookup"><span data-stu-id="b671e-452">string</span></span>|<span data-ttu-id="b671e-453">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-453">64 characters</span></span>||<span data-ttu-id="b671e-454">Type de commande.</span><span class="sxs-lookup"><span data-stu-id="b671e-454">Type of the command.</span></span> <span data-ttu-id="b671e-455">L’un `query` ou `action` l’autre de ou .</span><span class="sxs-lookup"><span data-stu-id="b671e-455">One of `query` or `action`.</span></span> <span data-ttu-id="b671e-456">Par défaut **: requête**.</span><span class="sxs-lookup"><span data-stu-id="b671e-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="b671e-457">string</span><span class="sxs-lookup"><span data-stu-id="b671e-457">string</span></span>|<span data-ttu-id="b671e-458">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-458">128 characters</span></span>||<span data-ttu-id="b671e-459">La description qui apparaît aux utilisateurs pour indiquer le but de cette commande.</span><span class="sxs-lookup"><span data-stu-id="b671e-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="b671e-460">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-460">boolean</span></span>|||<span data-ttu-id="b671e-461">Une valeur boolean indique si la commande s’exécute initialement sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="b671e-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="b671e-462">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="b671e-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="b671e-463">tableau de cordes</span><span class="sxs-lookup"><span data-stu-id="b671e-463">array of Strings</span></span>|<span data-ttu-id="b671e-464">3</span><span class="sxs-lookup"><span data-stu-id="b671e-464">3</span></span>||<span data-ttu-id="b671e-465">Définit d’où l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="b671e-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="b671e-466">Toute combinaison de `compose` , `commandBox` . `message`</span><span class="sxs-lookup"><span data-stu-id="b671e-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="b671e-467">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="b671e-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="b671e-468">booléen</span><span class="sxs-lookup"><span data-stu-id="b671e-468">boolean</span></span>|||<span data-ttu-id="b671e-469">Une valeur boolean qui indique si elle doit aller chercher le module de tâche dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="b671e-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="b671e-470">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="b671e-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="b671e-471">objet</span><span class="sxs-lookup"><span data-stu-id="b671e-471">object</span></span>|||<span data-ttu-id="b671e-472">Spécifiez le module de tâches à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="b671e-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="b671e-473">string</span><span class="sxs-lookup"><span data-stu-id="b671e-473">string</span></span>|<span data-ttu-id="b671e-474">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-474">64 characters</span></span>||<span data-ttu-id="b671e-475">Titre de dialogue initial.</span><span class="sxs-lookup"><span data-stu-id="b671e-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="b671e-476">string</span><span class="sxs-lookup"><span data-stu-id="b671e-476">string</span></span>|||<span data-ttu-id="b671e-477">Largeur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».</span><span class="sxs-lookup"><span data-stu-id="b671e-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="b671e-478">string</span><span class="sxs-lookup"><span data-stu-id="b671e-478">string</span></span>|||<span data-ttu-id="b671e-479">Hauteur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».</span><span class="sxs-lookup"><span data-stu-id="b671e-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="b671e-480">string</span><span class="sxs-lookup"><span data-stu-id="b671e-480">string</span></span>|||<span data-ttu-id="b671e-481">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="b671e-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="b671e-482">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-482">array of object</span></span>|<span data-ttu-id="b671e-483">5 articles</span><span class="sxs-lookup"><span data-stu-id="b671e-483">5 items</span></span>|<span data-ttu-id="b671e-484">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-484">✔</span></span>|<span data-ttu-id="b671e-485">La liste des paramètres de la commande prend.</span><span class="sxs-lookup"><span data-stu-id="b671e-485">The list of parameters the command takes.</span></span> <span data-ttu-id="b671e-486">Minimum: 1; maximum: 5.</span><span class="sxs-lookup"><span data-stu-id="b671e-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="b671e-487">string</span><span class="sxs-lookup"><span data-stu-id="b671e-487">string</span></span>|<span data-ttu-id="b671e-488">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-488">64 characters</span></span>|<span data-ttu-id="b671e-489">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-489">✔</span></span>|<span data-ttu-id="b671e-490">Le nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="b671e-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="b671e-491">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="b671e-492">string</span><span class="sxs-lookup"><span data-stu-id="b671e-492">string</span></span>|<span data-ttu-id="b671e-493">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-493">32 characters</span></span>|<span data-ttu-id="b671e-494">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-494">✔</span></span>|<span data-ttu-id="b671e-495">Titre convivial pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="b671e-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="b671e-496">string</span><span class="sxs-lookup"><span data-stu-id="b671e-496">string</span></span>|<span data-ttu-id="b671e-497">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-497">128 characters</span></span>||<span data-ttu-id="b671e-498">Chaîne conviviale qui décrit le but de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="b671e-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="b671e-499">string</span><span class="sxs-lookup"><span data-stu-id="b671e-499">string</span></span>|<span data-ttu-id="b671e-500">512 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-500">512 characters</span></span>||<span data-ttu-id="b671e-501">Valeur initiale pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="b671e-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="b671e-502">string</span><span class="sxs-lookup"><span data-stu-id="b671e-502">string</span></span>|<span data-ttu-id="b671e-503">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-503">128 characters</span></span>||<span data-ttu-id="b671e-504">Définit le type de contrôle affiché sur un module de tâches pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="b671e-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="b671e-505">L’un des `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b671e-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="b671e-506">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-506">array of objects</span></span>|<span data-ttu-id="b671e-507">10 articles</span><span class="sxs-lookup"><span data-stu-id="b671e-507">10 items</span></span>||<span data-ttu-id="b671e-508">Les options de choix pour le `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b671e-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="b671e-509">Utilisez seulement quand `parameter.inputType` est `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b671e-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="b671e-510">string</span><span class="sxs-lookup"><span data-stu-id="b671e-510">string</span></span>|<span data-ttu-id="b671e-511">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-511">128 characters</span></span>|<span data-ttu-id="b671e-512">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-512">✔</span></span>|<span data-ttu-id="b671e-513">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="b671e-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="b671e-514">string</span><span class="sxs-lookup"><span data-stu-id="b671e-514">string</span></span>|<span data-ttu-id="b671e-515">512 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-515">512 characters</span></span>|<span data-ttu-id="b671e-516">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-516">✔</span></span>|<span data-ttu-id="b671e-517">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="b671e-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="b671e-518">autorisations</span><span class="sxs-lookup"><span data-stu-id="b671e-518">permissions</span></span>

<span data-ttu-id="b671e-519">**Facultatif** — gamme de chaînes</span><span class="sxs-lookup"><span data-stu-id="b671e-519">**Optional** — array of strings</span></span>

<span data-ttu-id="b671e-520">Un tableau de `string` ce qui spécifie les autorisations des demandes d’application, ce qui permet aux utilisateurs finaux de savoir comment l’extension fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b671e-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="b671e-521">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="b671e-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="b671e-522">`identity`&emsp;Nécessite des informations d’identité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-522">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="b671e-523">`messageTeamMembers`&emsp;Nécessite la permission d’envoyer des messages directs aux membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="b671e-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="b671e-524">La modification de ces autorisations lors de la mise à jour de l’application, provoque vos utilisateurs à répéter le processus de consentement après avoir exécuté l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b671e-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="b671e-525">Voir Mise [à jour de votre application pour](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b671e-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="b671e-526">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="b671e-526">devicePermissions</span></span>

<span data-ttu-id="b671e-527">**Facultatif** — gamme de chaînes</span><span class="sxs-lookup"><span data-stu-id="b671e-527">**Optional** — array of strings</span></span>

<span data-ttu-id="b671e-528">Fournit les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application demande l’accès.</span><span class="sxs-lookup"><span data-stu-id="b671e-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="b671e-529">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="b671e-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="b671e-530">validDomains (en)</span><span class="sxs-lookup"><span data-stu-id="b671e-530">validDomains</span></span>

<span data-ttu-id="b671e-531">**Facultatif,** sauf requis **lorsqu’il** est noté.</span><span class="sxs-lookup"><span data-stu-id="b671e-531">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="b671e-532">Une liste de domaines valides pour les sites Web que l’application s’attend à charger au sein Teams client.</span><span class="sxs-lookup"><span data-stu-id="b671e-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="b671e-533">Les listes de domaines peuvent inclure des wildcards, par `*.example.com` exemple, .</span><span class="sxs-lookup"><span data-stu-id="b671e-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="b671e-534">Cela correspond exactement à un segment du domaine; si vous avez besoin de `a.b.example.com` correspondre, puis utiliser `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="b671e-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="b671e-535">Si votre configuration d’onglet ou interface utilisateur de contenu doit naviguer vers n’importe quel autre domaine en dehors de l’une des utilisations pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="b671e-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="b671e-536">Il **n’est** pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="b671e-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="b671e-537">Par exemple, pour authentifier à l’aide d’un identifiant Google, il est nécessaire de rediriger vers accounts.google.com, cependant, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="b671e-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="b671e-538">Teams applications qui nécessitent que leurs propres URL sharepoint fonctionnent bien, inclut « {teamsitedomain} » dans leur liste de domaine valide.</span><span class="sxs-lookup"><span data-stu-id="b671e-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b671e-539">N’ajoutez pas de domaines qui sont hors de votre contrôle, que ce soit directement ou par wildcards.</span><span class="sxs-lookup"><span data-stu-id="b671e-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="b671e-540">Par exemple, `yourapp.onmicrosoft.com` est valide, cependant, `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="b671e-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="b671e-541">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="b671e-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="b671e-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="b671e-542">webApplicationInfo</span></span>

<span data-ttu-id="b671e-543">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-543">**Optional** — object</span></span>

<span data-ttu-id="b671e-544">Fournissez à Azure Active Directory d’application (AAD) et aux informations Graph Microsoft pour aider les utilisateurs à se connecter de manière transparente à votre application.</span><span class="sxs-lookup"><span data-stu-id="b671e-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="b671e-545">Si votre application est enregistrée dans AAD, vous devez fournir l’ID App, afin que les administrateurs puissent facilement examiner les autorisations et accorder le consentement dans Teams d’administration.</span><span class="sxs-lookup"><span data-stu-id="b671e-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="b671e-546">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-546">Name</span></span>| <span data-ttu-id="b671e-547">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-547">Type</span></span>| <span data-ttu-id="b671e-548">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-548">Maximum size</span></span> | <span data-ttu-id="b671e-549">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-549">Required</span></span> | <span data-ttu-id="b671e-550">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b671e-551">string</span><span class="sxs-lookup"><span data-stu-id="b671e-551">string</span></span>|<span data-ttu-id="b671e-552">36 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-552">36 characters</span></span>|<span data-ttu-id="b671e-553">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-553">✔</span></span>|<span data-ttu-id="b671e-554">Id d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-554">AAD application id of the app.</span></span> <span data-ttu-id="b671e-555">Cet id doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="b671e-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="b671e-556">string</span><span class="sxs-lookup"><span data-stu-id="b671e-556">string</span></span>|<span data-ttu-id="b671e-557">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-557">2048 characters</span></span>|<span data-ttu-id="b671e-558">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-558">✔</span></span>|<span data-ttu-id="b671e-559">URL de ressources de l’application pour l’acquisition de jetons auth pour SSO.</span><span class="sxs-lookup"><span data-stu-id="b671e-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="b671e-560">**REMARQUE:** Si vous n’utilisez pas SSO, assurez-vous d’entrer une valeur de chaîne factice dans ce champ au manifeste de votre application, par exemple, https://notapplicable pour éviter une réponse d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b671e-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="b671e-561">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b671e-561">array of strings</span></span>|<span data-ttu-id="b671e-562">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-562">128 characters</span></span>||<span data-ttu-id="b671e-563">Spécifiez [le consentement spécifique de ressource](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)granulaire.</span><span class="sxs-lookup"><span data-stu-id="b671e-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="b671e-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="b671e-564">showLoadingIndicator</span></span>

<span data-ttu-id="b671e-565">**Facultatif** — boolean</span><span class="sxs-lookup"><span data-stu-id="b671e-565">**Optional** — boolean</span></span>

<span data-ttu-id="b671e-566">Indique s’il y a ou non un indicateur de chargement lorsqu’une application ou un onglet est en train de charger.</span><span class="sxs-lookup"><span data-stu-id="b671e-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="b671e-567">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="b671e-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="b671e-568">Si vous `showLoadingIndicator` sélectionnez comme vrai dans le manifeste de votre application, pour charger correctement la page, modifiez les pages de contenu de vos onglets et modules de tâches tels que décrits dans Afficher un document [indicateur de chargement](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) natif.</span><span class="sxs-lookup"><span data-stu-id="b671e-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="b671e-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="b671e-569">isFullScreen</span></span>

 <span data-ttu-id="b671e-570">**Facultatif** — boolean</span><span class="sxs-lookup"><span data-stu-id="b671e-570">**Optional** — boolean</span></span>

<span data-ttu-id="b671e-571">Indiquez où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b671e-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="b671e-572">La valeur par défaut est **False**.</span><span class="sxs-lookup"><span data-stu-id="b671e-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="b671e-573">activités</span><span class="sxs-lookup"><span data-stu-id="b671e-573">activities</span></span>

<span data-ttu-id="b671e-574">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="b671e-574">**Optional** — object</span></span>

<span data-ttu-id="b671e-575">Définissez les propriétés que votre application utilise pour publier un flux d’activité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b671e-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="b671e-576">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-576">Name</span></span>| <span data-ttu-id="b671e-577">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-577">Type</span></span>| <span data-ttu-id="b671e-578">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-578">Maximum size</span></span> | <span data-ttu-id="b671e-579">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-579">Required</span></span> | <span data-ttu-id="b671e-580">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="b671e-581">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b671e-581">array of Objects</span></span>|<span data-ttu-id="b671e-582">128 articles</span><span class="sxs-lookup"><span data-stu-id="b671e-582">128 items</span></span>| | <span data-ttu-id="b671e-583">Fournissez les types d’activités que votre application peut publier sur un flux d’activité des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b671e-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="b671e-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="b671e-584">activities.activityTypes</span></span>

|<span data-ttu-id="b671e-585">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-585">Name</span></span>| <span data-ttu-id="b671e-586">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-586">Type</span></span>| <span data-ttu-id="b671e-587">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-587">Maximum size</span></span> | <span data-ttu-id="b671e-588">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-588">Required</span></span> | <span data-ttu-id="b671e-589">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="b671e-590">string</span><span class="sxs-lookup"><span data-stu-id="b671e-590">string</span></span>|<span data-ttu-id="b671e-591">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-591">32 characters</span></span>|<span data-ttu-id="b671e-592">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-592">✔</span></span>|<span data-ttu-id="b671e-593">Le type de notification.</span><span class="sxs-lookup"><span data-stu-id="b671e-593">The notification type.</span></span> <span data-ttu-id="b671e-594">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="b671e-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="b671e-595">string</span><span class="sxs-lookup"><span data-stu-id="b671e-595">string</span></span>|<span data-ttu-id="b671e-596">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-596">128 characters</span></span>|<span data-ttu-id="b671e-597">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-597">✔</span></span>|<span data-ttu-id="b671e-598">Une brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="b671e-598">A brief description of the notification.</span></span> <span data-ttu-id="b671e-599">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="b671e-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="b671e-600">string</span><span class="sxs-lookup"><span data-stu-id="b671e-600">string</span></span>|<span data-ttu-id="b671e-601">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b671e-601">128 characters</span></span>|<span data-ttu-id="b671e-602">✔</span><span class="sxs-lookup"><span data-stu-id="b671e-602">✔</span></span>|<span data-ttu-id="b671e-603">Ex: « {actor} créé tâche {taskId} pour vous »</span><span class="sxs-lookup"><span data-stu-id="b671e-603">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="b671e-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="b671e-604">defaultInstallScope</span></span>

<span data-ttu-id="b671e-605">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="b671e-605">**Optional** - string</span></span>

<span data-ttu-id="b671e-606">Spécifie la portée d’installation définie pour cette application par défaut.</span><span class="sxs-lookup"><span data-stu-id="b671e-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="b671e-607">La portée définie sera l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="b671e-608">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="b671e-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="b671e-609">defaultGroupCapability (en)</span><span class="sxs-lookup"><span data-stu-id="b671e-609">defaultGroupCapability</span></span>

<span data-ttu-id="b671e-610">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="b671e-610">**Optional** - object</span></span>

<span data-ttu-id="b671e-611">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la capacité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="b671e-612">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="b671e-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="b671e-613">Nom</span><span class="sxs-lookup"><span data-stu-id="b671e-613">Name</span></span>| <span data-ttu-id="b671e-614">Type</span><span class="sxs-lookup"><span data-stu-id="b671e-614">Type</span></span>| <span data-ttu-id="b671e-615">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b671e-615">Maximum size</span></span> | <span data-ttu-id="b671e-616">Requis</span><span class="sxs-lookup"><span data-stu-id="b671e-616">Required</span></span> | <span data-ttu-id="b671e-617">Description</span><span class="sxs-lookup"><span data-stu-id="b671e-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="b671e-618">string</span><span class="sxs-lookup"><span data-stu-id="b671e-618">string</span></span>|||<span data-ttu-id="b671e-619">Lorsque la portée d’installation sélectionnée `team` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="b671e-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="b671e-620">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="b671e-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="b671e-621">string</span><span class="sxs-lookup"><span data-stu-id="b671e-621">string</span></span>|||<span data-ttu-id="b671e-622">Lorsque la portée d’installation sélectionnée `groupchat` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="b671e-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="b671e-623">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="b671e-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="b671e-624">string</span><span class="sxs-lookup"><span data-stu-id="b671e-624">string</span></span>|||<span data-ttu-id="b671e-625">Lorsque la portée d’installation sélectionnée `meetings` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="b671e-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="b671e-626">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="b671e-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="b671e-627">configurablesProperties</span><span class="sxs-lookup"><span data-stu-id="b671e-627">configurableProperties</span></span>

<span data-ttu-id="b671e-628">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="b671e-628">**Optional** - array</span></span>

<span data-ttu-id="b671e-629">Le `configurableProperties` bloc définit les propriétés de l’application Teams’administrateur peut personnaliser.</span><span class="sxs-lookup"><span data-stu-id="b671e-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="b671e-630">Pour plus d’informations, [consultez les applications personnalisées dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="b671e-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="b671e-631">Un minimum d’une propriété doit être défini.</span><span class="sxs-lookup"><span data-stu-id="b671e-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="b671e-632">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="b671e-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="b671e-633">En tant que meilleure pratique, vous devez fournir des directives de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="b671e-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="b671e-634">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b671e-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="b671e-635">`name`: Permet à l’administrateur de modifier le nom d’affichage de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="b671e-636">`shortDescription`: Permet à l’administrateur de modifier la courte description de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="b671e-637">`longDescription`: Permet à l’administrateur de modifier la description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="b671e-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="b671e-638">`smallImageUrl`: C’est `outline` la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="b671e-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="b671e-639">`largeImageUrl`: C’est `color` la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="b671e-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="b671e-640">`accentColor`: C’est la couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.</span><span class="sxs-lookup"><span data-stu-id="b671e-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="b671e-641">`websiteUrl`: Il s’agit https://'URL du site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="b671e-642">`privacyUrl`: Il s’agit https://'URL de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="b671e-643">`termsOfUseUrl`: C’est https:// URL aux conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="b671e-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


