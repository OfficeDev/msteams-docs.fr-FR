---
title: Configurer les fournisseurs d’identité OAuth 2.0
description: Décrit comment configurer des fournisseurs d’identité axés sur Azure AD
ms.topic: how-to
localization_priority: Normal
keywords: Fournisseur d’identité oauth AAD d’authentification teams
ms.openlocfilehash: ffcf376ea6c4f1a94d797413af22af867dbd5b53
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020855"
---
# <a name="configure-identity-providers"></a><span data-ttu-id="2f42a-104">Configurer les fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="2f42a-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="2f42a-105">Configuration d’une application pour utiliser Azure Active Directory comme fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="2f42a-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="2f42a-106">Les fournisseurs d’identité qui la prise en charge d’OAuth 2.0 n’authentifiera pas les demandes provenant d’applications inconnues ; les applications doivent être inscrites à l’avance.</span><span class="sxs-lookup"><span data-stu-id="2f42a-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="2f42a-107">Pour ce faire avec Azure AD, suivez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f42a-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="2f42a-108">Ouvrez le [portail d’inscription des applications.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)</span><span class="sxs-lookup"><span data-stu-id="2f42a-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="2f42a-109">Sélectionnez votre application pour afficher ses propriétés ou cliquez sur le bouton « Nouvelle inscription ».</span><span class="sxs-lookup"><span data-stu-id="2f42a-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="2f42a-110">Recherchez la section **URI de** redirection pour l’application.</span><span class="sxs-lookup"><span data-stu-id="2f42a-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="2f42a-111">Dans le menu déroulant, assurez-vous **que le site Web** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2f42a-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="2f42a-112">Mettez à jour l’URL de votre point de terminaison d’authentification.</span><span class="sxs-lookup"><span data-stu-id="2f42a-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="2f42a-113">Pour les exemples d’applications TypeScript/Node.js et C# sur GitHub, les URL de redirection seront similaires à ceci :</span><span class="sxs-lookup"><span data-stu-id="2f42a-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="2f42a-114">Rediriger les URL : `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="2f42a-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="2f42a-115">Remplacez `<hostname>` par votre hôte réel.</span><span class="sxs-lookup"><span data-stu-id="2f42a-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="2f42a-116">Il peut s’agit d’un site d’hébergement dédié tel qu’Azure, Glitch ou un tunnel ngrok vers localhost sur votre ordinateur de développement tel que `abcd1234.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="2f42a-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="2f42a-117">Vous n’avez peut-être pas encore ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.</span><span class="sxs-lookup"><span data-stu-id="2f42a-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="2f42a-118">Autres fournisseurs d’authentification</span><span class="sxs-lookup"><span data-stu-id="2f42a-118">Other authentication providers</span></span>

* <span data-ttu-id="2f42a-119">**LinkedIn** Suivez les instructions de [configuration de votre application LinkedIn](/linkedin/talent/apply-with-linkedin)</span><span class="sxs-lookup"><span data-stu-id="2f42a-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](/linkedin/talent/apply-with-linkedin)</span></span>

* <span data-ttu-id="2f42a-120">**Google** Obtenir les informations d’identification du client OAuth 2.0 à partir de la [console d’API Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="2f42a-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
