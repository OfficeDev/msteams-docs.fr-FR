---
title: Réorganiser les onglets d’applications personnelles
description: Comment réorganiser les onglets statiques d’application personnelle dans votre application personnelle
keywords: développement d’onglets teams
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554826"
---
# <a name="reorder-personal-app-tabs"></a><span data-ttu-id="8e356-104">Réorganiser les onglets d’applications personnelles</span><span class="sxs-lookup"><span data-stu-id="8e356-104">Reorder personal app tabs</span></span>

<span data-ttu-id="8e356-105">À partir de la version de manifeste 1,7, les développeurs peuvent réorganiser tous les onglets dans leur application personnelle.</span><span class="sxs-lookup"><span data-stu-id="8e356-105">Starting with manifest version 1.7 developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="8e356-106">En particulier, un développeur peut déplacer l’onglet « robots chat » (qui a toujours la première position par défaut) n’importe où dans l’en-tête de l’onglet de l’application personnelle.</span><span class="sxs-lookup"><span data-stu-id="8e356-106">In particular, a developer can move the “bot chat” tab (which has always defaulted to the first position) anywhere in the personal app tab header.</span></span> <span data-ttu-id="8e356-107">Nous avons déclaré deux mots clés de entityId de tabulation réservés : « conversations » et « à propos de ».</span><span class="sxs-lookup"><span data-stu-id="8e356-107">We’ve declared two reserved tab entityId keywords: “conversations” and “about”.</span></span>

## <a name="moving-the-chatconversation-tab"></a><span data-ttu-id="8e356-108">Déplacez l’onglet « conversation/conversation »</span><span class="sxs-lookup"><span data-stu-id="8e356-108">Moving the “Chat/Conversation” tab</span></span>

<span data-ttu-id="8e356-109">Si vous créez un bot avec une étendue « personnelle », il s’affiche toujours dans la première tabulation dans une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="8e356-109">If you create a bot with a “personal” scope, it will always show up in the first tab position in a personal app.</span></span> <span data-ttu-id="8e356-110">Si vous souhaitez la déplacer vers une autre position, vous devez ajouter un objet d’onglet statique à votre manifeste avec le mot clé réservé « conversations ».</span><span class="sxs-lookup"><span data-stu-id="8e356-110">If you wish to move it to another position, you need to add a static tab object to your manifest with the reserved keyword “conversations”.</span></span> <span data-ttu-id="8e356-111">Quel que soit l’endroit où vous ajoutez l’onglet « conversations » dans le tableau « staticTabs », c’est l’onglet de conversation qui apparaîtra sur le Web et le bureau.</span><span class="sxs-lookup"><span data-stu-id="8e356-111">Wherever you add the “conversations” tab in the “staticTabs” array, that’s where the conversation tab will appear on web and desktop.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> <span data-ttu-id="8e356-112">Notez que ce comportement n’est pas reflété sur mobile, étant donné que la conversation de robots personnel dispose déjà d’un emplacement dédié au sein de l’application personnelle.</span><span class="sxs-lookup"><span data-stu-id="8e356-112">Note that this behavior is not reflected on mobile since the personal bot chat already has a dedicated place within the personal app.</span></span>

## <a name="moving-the-about-tab"></a><span data-ttu-id="8e356-113">Mouvement de l’onglet « à propos de »</span><span class="sxs-lookup"><span data-stu-id="8e356-113">Moving the “About” tab</span></span>

<span data-ttu-id="8e356-114">L’onglet « à propos de » est toujours défini par défaut à la fin de la barre d’en-tête d’onglet de l’application personnelle.</span><span class="sxs-lookup"><span data-stu-id="8e356-114">The “About” tab always defaults to the end of the personal app tab header bar.</span></span> <span data-ttu-id="8e356-115">Si vous souhaitez la déplacer vers une autre position, vous devez utiliser la entityId « à propos de ».</span><span class="sxs-lookup"><span data-stu-id="8e356-115">If you wish to move it to another position, you need to use the “about” entityId.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> <span data-ttu-id="8e356-116">Notez que l’onglet à propos de n’est pas affiché sur mobile.</span><span class="sxs-lookup"><span data-stu-id="8e356-116">Note that the about tab is not shown on mobile.</span></span>

## <a name="example-code"></a><span data-ttu-id="8e356-117">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="8e356-117">Example code</span></span>

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
