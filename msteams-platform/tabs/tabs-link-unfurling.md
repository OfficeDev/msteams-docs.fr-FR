---
title: Déploiement du lien des onglets et vue des étapes
author: Rajeshwari-v
description: Découvrez comment déployer un lien, ouvrir le mode Étape et épingler un onglet avec Microsoft Teams application. Découvrez l’affichage intermédiaire et son appel à l’aide d’une carte adaptative à l’aide de l’exemple de code et de l’exemple.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 043129d6a81543ac00acf8b64da49f75282823a2
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104083"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Déploiement du lien des onglets et vue des étapes

La vue d’étape est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran dans Teams et épinglé sous forme d’onglet.

## <a name="stage-view"></a>Vue d’étape

La vue d’étape est un composant d’interface utilisateur en plein écran que vous pouvez appeler pour exposer votre contenu web. Le service de déploiement de liaison existant est mis à jour afin qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Lorsqu’un utilisateur envoie une URL dans une conversation ou un canal, l’URL est déployée vers une carte adaptative. L’utilisateur peut sélectionner **Affichage** dans la carte et épingler le contenu sous la forme d’un onglet directement à partir de l’affichage étape.

## <a name="advantage-of-stage-view"></a>Avantage de l’affichage de l’étape

La vue d’étape permet d’obtenir une expérience plus transparente de l’affichage du contenu dans Teams. Les utilisateurs peuvent ouvrir et afficher le contenu fourni par votre application sans quitter le contexte, et ils peuvent épingler le contenu à la conversation ou au canal pour un accès rapide ultérieur, ce qui entraîne un plus grand engagement de l’utilisateur avec votre application.

## <a name="stage-view-vs-task-module"></a>Vue d’étape et module de tâche

|Vue d’étape|Module de tâche|
|:-----------|:-----------|
|L’affichage intermédiaire est utile lorsque vous avez du contenu enrichi à afficher aux utilisateurs, par exemple une page, un tableau de bord, un fichier, etc. Il fournit des fonctionnalités enrichies qui permettent d’afficher votre contenu dans le canevas en plein écran.|[Le module de tâche](../task-modules-and-cards/task-modules/task-modules-tabs.md) est particulièrement utile pour afficher les messages qui nécessitent l’attention de l’utilisateur ou collecter les informations nécessaires pour passer à l’étape suivante.|
  
## <a name="invoke-stage-view"></a>Appeler l’affichage d’étape

Vous pouvez appeler la vue d’étape de la manière suivante :

* [Appeler la vue d’étape à partir d’une carte adaptative](#invoke-stage-view-from-adaptive-card)
* [Appeler la vue d’étape par le biais d’un lien profond](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Appeler la vue d’étape à partir d’une carte adaptative

Lorsque l’utilisateur entre une URL sur le client de bureau Teams, le bot est appelé et retourne une [carte adaptative](../task-modules-and-cards/cards/cards-actions.md) avec la possibilité d’ouvrir l’URL dans une phase. Une fois qu’une étape est lancée et fournie `tabInfo` , vous pouvez ajouter la possibilité d’épingler la phase sous forme d’onglet.  

Les images suivantes affichent une étape ouverte à partir d’une carte adaptative :

[![Ouvrir une étape à partir d’une carte adaptative](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Ouvrir une étape](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

### <a name="example"></a>Exemple

Voici le code permettant d’ouvrir une étape à partir d’une carte adaptative :

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

Le `invoke` type de requête doit être `composeExtension/queryLink`.

> [!NOTE]
>
> * `invoke` le flux de travail est similaire au flux de travail actuel `appLinking` .
> * Pour maintenir la cohérence, il est recommandé de nommer `Action.Submit` `View`.
> * `websiteUrl` est une propriété obligatoire à transmettre dans l’objet `TabInfo` .

Voici le processus d’appel de la vue d’étape :

* Lorsque l’utilisateur sélectionne **Affichage**, le bot reçoit une `invoke` demande. Le type de requête est `composeExtension/queryLink`.
* `invoke` la réponse du bot contient une carte adaptative avec le type `tab/tabInfoAction` qu’elle contient.
* Le bot répond avec un `200` code.

> [!NOTE]
> Sur Teams clients mobiles, l’appel de l’affichage intermédiaire pour les applications distribuées par le biais du [magasin Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) et l’absence d’expérience optimisée pour Moblie ouvre le navigateur web par défaut de l’appareil. Le navigateur ouvre l’URL spécifiée dans le `websiteUrl` paramètre de l’objet `TabInfo` .

## <a name="invoke-stage-view-through-deep-link"></a>Appeler la vue d’étape par le biais d’un lien profond

Pour appeler la vue d’étape via un lien profond à partir de votre onglet, vous devez encapsuler l’URL de lien profond dans l’API `microsoftTeams.executeDeeplink(url)` . Le lien profond peut également être transmis par le biais d’une `OpenURL` action dans la carte.

### <a name="syntax"></a>Syntaxe

Voici la syntaxe de lien profond :

https://teams.microsoft.com/l/stage/{appId}/0?context={« contentUrl »:"contentUrl »,"websiteUrl »:"websiteUrl »,"name »:"Contoso"}
 
### <a name="examples"></a>Exemples

Lorsqu’un utilisateur entre une URL, elle est déployée dans une carte adaptative.

Voici les exemples de liens profonds permettant d’appeler la vue d’étape :

**Exemple 1 : URL avec threadId**

URL non codée :

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={« contentUrl »: »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl »: »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title »:"Quotes:Miscellaneous »,"threadId »:"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

URL encodée :

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**Exemple 2 : URL sans threadId**

URL non codée :

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={« contentUrl »: »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl »: »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title »:"Quotes:Miscellaneous"}

Encodé

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> Tous les liens profonds doivent être encodés avant de coller l’URL. Nous ne prenons pas en charge les URL non codées.
>
> * L’option `name` est facultative dans le lien profond. S’il n’est pas inclus, le nom de l’application le remplace.
> * Le lien profond peut également être transmis par le biais d’une `OpenURL` action.
> * Lorsque vous lancez une phase à partir d’un certain contexte, assurez-vous que votre application fonctionne dans ce contexte. Par exemple, si votre mode Étape est lancé à partir d’une application personnelle, vous devez vous assurer que votre application a une étendue personnelle.

## <a name="tab-information-property"></a>Tab information, propriété

| Nom de la propriété | Type | Nombre de caractères | Description |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Chaîne | 64 | Cette propriété est un identificateur unique pour l’entité affichée par l’onglet. Ce champ est obligatoire.|
| `name` | Chaîne | 128 | Cette propriété est le nom complet de l’onglet dans l’interface de canal. Ce champ est facultatif.|
| `contentUrl` | Chaîne | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans le canevas Teams. Ce champ est obligatoire.|
| `websiteUrl?` | Chaîne | 2048 | Cette propriété est l’URL https:// vers laquelle pointer, si un utilisateur choisit d’afficher dans un navigateur. Ce champ est obligatoire.|
| `removeUrl?` | Chaîne | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur à afficher lorsque l’utilisateur supprime l’onglet. Il s’agit d’un champ facultatif.|

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Tabulation en mode étape |Microsoft Teams’exemple d’application d’onglet pour illustrer l’onglet en mode étape.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Déploiement de liens d’extensions de message](~/messaging-extensions/how-to/link-unfurling.md)
* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un canal ou un onglet de groupe](~/tabs/how-to/create-channel-group-tab.md)
