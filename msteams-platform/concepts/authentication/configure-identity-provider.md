---
title: Configuration des fournisseurs d’identité OAuth 2,0
description: Décrit comment configurer des fournisseurs d’identité avec un focus sur Azure AD
keywords: authentification par teams fournisseur d’identité OAuth AAD
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673920"
---
# <a name="configuring-identity-providers"></a><span data-ttu-id="55da2-104">Configuration des fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="55da2-104">Configuring identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="55da2-105">Configuration d’une application pour utiliser Azure Active Directory en tant que fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="55da2-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="55da2-106">Les fournisseurs d’identité prenant en charge OAuth 2,0 n’authentifient pas les demandes provenant d’applications inconnues ; les applications doivent être enregistrées à l’avance.</span><span class="sxs-lookup"><span data-stu-id="55da2-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="55da2-107">Pour effectuer cette opération avec Azure AD, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="55da2-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="55da2-108">Ouvrez le [portail d’inscription des applications](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span><span class="sxs-lookup"><span data-stu-id="55da2-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="55da2-109">Sélectionnez votre application pour afficher ses propriétés, ou cliquez sur le bouton « nouvelle inscription ».</span><span class="sxs-lookup"><span data-stu-id="55da2-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="55da2-110">Recherchez la section **URI de redirection** pour l’application.</span><span class="sxs-lookup"><span data-stu-id="55da2-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="55da2-111">Dans le menu déroulant, vérifiez que l’option **Web** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="55da2-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="55da2-112">Mettez à jour l’URL vers votre point de terminaison d’authentification.</span><span class="sxs-lookup"><span data-stu-id="55da2-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="55da2-113">Pour les exemples d’applications de type machine à écrire/node. js et C# sur GitHub, les URL de redirection ressemblent à ceci :</span><span class="sxs-lookup"><span data-stu-id="55da2-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="55da2-114">URL de redirection :`https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="55da2-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="55da2-115">Remplacez `<hostname>` par votre hôte réel.</span><span class="sxs-lookup"><span data-stu-id="55da2-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="55da2-116">Il peut s’agir d’un site d’hébergement dédié, tel que Azure, un problème ou un tunnel ngrok vers localhost sur votre `abcd1234.ngrok.io`ordinateur de développement, comme.</span><span class="sxs-lookup"><span data-stu-id="55da2-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="55da2-117">Vous ne disposez peut-être pas encore de ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.</span><span class="sxs-lookup"><span data-stu-id="55da2-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="55da2-118">Autres fournisseurs d’authentification</span><span class="sxs-lookup"><span data-stu-id="55da2-118">Other authentication providers</span></span>

* <span data-ttu-id="55da2-119">**LinkedIn** Suivez les instructions de la procédure de [configuration de votre application LinkedIn](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="55da2-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="55da2-120">**Google** Obtenir des informations d’identification de client 2,0 OAuth à partir de la [console d’API Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="55da2-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
