---
title: Déploiement du lien des onglets et vue des étapes
author: Rajeshwari-v
description: Découvrez l’affichage intermédiaire, un composant d’interface utilisateur en plein écran appelé pour exposer votre contenu web. Le déploiement de liens est utilisé pour transformer les URL en un onglet à l’aide de cartes adaptatives.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 41fce323ff65dd264e8dca71120ea126ddfcf16f
ms.sourcegitcommit: 93c2fcd78a2fbb4550d180d295d98d1b3944ca67
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2022
ms.locfileid: "68484919"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Déploiement du lien des onglets et vue des étapes

La vue d’étape est un nouveau composant d’interface utilisateur. Il vous permet d’afficher le contenu qui est ouvert en plein écran dans Teams et épinglé sous forme d’onglet.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="stage-view"></a>Vue des étapes

La vue des étapes est un composant d’interface utilisateur en plein écran que vous pouvez utiliser pour exposer votre contenu web. Le service de déploiement de liaison existant est mis à jour afin qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Lorsqu’un utilisateur envoie une URL dans une conversation ou un canal, l’URL est déployée vers une carte adaptative. L’utilisateur peut sélectionner **Affichage** dans la carte et épingler le contenu sous la forme d’un onglet directement à partir de la vue des étapes.

## <a name="advantage-of-stage-view"></a>Avantage de la vue des étapes

Stage View helps provide a more seamless experience of viewing content in Teams. Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access leading to a higher user engagement with your app.

## <a name="stage-view-vs-task-module"></a>Vue des étapes et module de tâche

|Vue des étapes|Module de tâche|
|:-----------|:-----------|
|La vue des étapes est utile lorsque vous avez un contenu riche à afficher aux utilisateurs, comme une page, un tableau de bord, un fichier, etc. Il fournit des fonctionnalités enrichies qui permettent d’afficher votre contenu dans le canevas en plein écran.|[Le module de tâches](../task-modules-and-cards/task-modules/task-modules-tabs.md) est particulièrement utile pour afficher des messages qui requièrent l'attention de l'utilisateur, ou pour recueillir les informations nécessaires pour passer à l'étape suivante.|
  
## <a name="invoke-stage-view"></a>Invoquer la vue de scène

Vous pouvez invoquer la vue des étapes de la manière suivante :

* [Appeler vue des étapes depuis la carte adaptative](#invoke-stage-view-from-adaptive-card)
* [Appeler la vue des étapes par un lien profond](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Invoquer la vue des étapes à partir de la carte adaptative

Lorsque l'utilisateur saisit une URL sur le client de bureau Teams, le robot est invoqué et renvoie une [carte adaptative](../task-modules-and-cards/cards/cards-actions.md) avec l'option d'ouvrir l'URL dans une étape. Une fois qu'une étape est lancée et que l'étape est `tabInfo`fournie, vous pouvez ajouter la possibilité d'épingler l'étape comme un onglet.  

Les images suivantes montrent une scène ouverte à partir d'une carte adaptative :

[![Ouvrir une étape de la carte adaptative](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Ouvrir une étape](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

### <a name="example"></a>Exemple

Voici le code pour ouvrir une scène à partir d'une carte adaptative :

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

Le `invoke`type de demande doit être `composeExtension/queryLink`.

> [!NOTE]
>
> * `invoke`Le flux de travail est similaire au flux de `appLinking`travail actuel.
> * Pour maintenir la cohérence, il est recommandé `Action.Submit`d'attribuer un nom en tant que`View`.
> * `websiteUrl`est une propriété obligatoire à passer dans `TabInfo`l'objet.

Voici le processus d’appel de la vue d’étape :

* When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
* `invoke` La réponse du robot contient une carte adaptative `tab/tabInfoAction`avec le type.
* Le robot répond avec un `200` code.

> [!NOTE]
>
> Sur les clients mobiles Teams, l’appel de la vue intermédiaire pour les applications distribuées via le [magasin Teams](~/concepts/deploy-and-publish/apps-publish-overview.md) et l’absence d’expérience optimisée pour les appareils mobiles ouvre le navigateur web par défaut de l’appareil. Le navigateur ouvre l'URL spécifié dans le `websiteUrl`paramètre de `TabInfo`l'objet.

## <a name="invoke-stage-view-through-deep-link"></a>Invoquer la vue des étapes par le biais d'un lien profond

Pour invoquer la vue des étapes par le biais d'un lien profond depuis votre onglet, vous devez intégrer l'URL du lien profond dans `app.openLink(url)`l'API. Le lien profond peut également être transmis par une `OpenURL`action dans la carte.

### <a name="syntax"></a>Syntaxe

Voici la syntaxe de lien profond :

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

### <a name="examples"></a>Exemples

Lorsqu’un utilisateur entre une URL, elle est déployée dans une carte adaptative.

Voici des exemples de liens profonds pour invoquer la vue des étapes :

**Exemple 1 : URL avec threadId**

URL non codée :

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

URL codée :

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

**Exemple 2 : URL sans threadId**

URL non codée :

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

Encodé

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

> [!NOTE]
> Tous les liens profonds doivent être encodés avant de coller l’URL. Nous ne prenons pas en charge les URL non codées.
>
> * Le `name`est facultatif en lien profond. S'il n'est pas inclus, le nom de l'application le remplace.
> * Le lien profond peut également être transmis par une `OpenURL`action.
> * Lorsque vous lancez une étape à partir d'un certain contexte, assurez-vous que votre application fonctionne dans ce contexte. Par exemple, si votre vue des étapes est lancée à partir d'une application personnelle, vous devez vous assurer que votre application a une portée personnelle.

## <a name="tab-information-property"></a>Propriété de l'information de l'onglet

| Nom de la propriété | Type | Nombre de caractères | Description |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Chaîne | 64 | Cette propriété est un identifiant unique pour l'entité que l'onglet affiche. Ce champ est obligatoire.|
| `name` | Chaîne | 128 | Cette propriété est le nom d'affichage de l'onglet dans l'interface du canal. Ce champ est facultatif.|
| `contentUrl` | Chaîne | 2048 | This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas. This is a required field.|
| `websiteUrl?` | Chaîne | 2048 | This property is the https:// URL to point at, if a user selects to view in a browser. This is a required field.|
| `removeUrl?` | Chaîne | 2048 | Cette propriété est l'URL https:// qui pointe vers l'interface utilisateur à afficher lorsque l'utilisateur supprime l'onglet. Il s'agit d'un champ facultatif.|

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Onglet dans la vue de l'étape |Exemple d'application d'onglet Microsoft Teams pour la démonstration de l'onglet dans la vue des étapes.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Déploiement du lien des extensions de message](~/messaging-extensions/how-to/link-unfurling.md)
* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
