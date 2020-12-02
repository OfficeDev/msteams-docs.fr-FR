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
# <a name="reorder-personal-app-tabs"></a>Réorganiser les onglets d’applications personnelles

À partir de la version de manifeste 1,7, les développeurs peuvent réorganiser tous les onglets dans leur application personnelle. En particulier, un développeur peut déplacer l’onglet « robots chat » (qui a toujours la première position par défaut) n’importe où dans l’en-tête de l’onglet de l’application personnelle. Nous avons déclaré deux mots clés de entityId de tabulation réservés : « conversations » et « à propos de ».

## <a name="moving-the-chatconversation-tab"></a>Déplacez l’onglet « conversation/conversation »

Si vous créez un bot avec une étendue « personnelle », il s’affiche toujours dans la première tabulation dans une application personnelle. Si vous souhaitez la déplacer vers une autre position, vous devez ajouter un objet d’onglet statique à votre manifeste avec le mot clé réservé « conversations ». Quel que soit l’endroit où vous ajoutez l’onglet « conversations » dans le tableau « staticTabs », c’est l’onglet de conversation qui apparaîtra sur le Web et le bureau. 

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
> Notez que ce comportement n’est pas reflété sur mobile, étant donné que la conversation de robots personnel dispose déjà d’un emplacement dédié au sein de l’application personnelle.

## <a name="moving-the-about-tab"></a>Mouvement de l’onglet « à propos de »

L’onglet « à propos de » est toujours défini par défaut à la fin de la barre d’en-tête d’onglet de l’application personnelle. Si vous souhaitez la déplacer vers une autre position, vous devez utiliser la entityId « à propos de ».

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
> Notez que l’onglet à propos de n’est pas affiché sur mobile.

## <a name="example-code"></a>Exemple de code

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
