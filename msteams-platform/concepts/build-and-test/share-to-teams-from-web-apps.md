---
title: Partager vers Teams à partir d’applications web
description: Découvrez comment ajouter le bouton Partager à Teams incorporé sur votre site web, avec un aperçu du site web, à l’aide d’exemples de code
ms.topic: reference
ms.localizationpriority: medium
keywords: Partager Teams partager sur Teams
ms.openlocfilehash: ac08d3c697bc5f02eb8527d2239afe022cb421af
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685668"
---
# <a name="share-to-teams-from-web-apps"></a>Partager vers Teams à partir d’applications web

Les sites web tiers peuvent utiliser le script de lancement pour incorporer Share à Teams boutons sur leurs pages web. Lorsque vous sélectionnez, il lance l’expérience Partager pour Teams dans une fenêtre contextuelle. Cela vous permet de partager un lien directement vers n’importe quelle personne ou Microsoft Teams canal sans changer de contexte. Ce document vous guide dans la création et l’incorporation d’un bouton Partager vers Teams pour votre site web, créer la préversion de votre site web et étendre Share à Teams pour l'éducation.

> [!NOTE]
>
> * Seules les versions de bureau de MicrosoftEdge&nbsp; et Google Chrome sont prises en charge.
> * L’utilisation de Freemium ou de comptes invités n’est pas prise en charge.  

L’image suivante affiche le partage pour Teams expérience contextuelle :

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Partager vers Teams fenêtre contextuelle":::

## <a name="embed-a-share-to-teams-button"></a>Incorporer un partage à Teams bouton

1. Ajoutez le `launcher.js` script sur votre page web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Ajoutez un élément HTML sur votre page web avec l’attribut `teams-share-button` de classe et le lien à partager dans l’attribut `data-href` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Une fois cette opération terminée, l’icône Microsoft Teams est ajoutée à votre site web. L’image suivante montre l’icône Partager vers Teams :

    ![Icône Partager vers Teams](~/assets/icons/share-to-teams-icon.png)

1. Sinon, si vous souhaitez une taille d’icône différente pour le bouton Partager pour Teams, utilisez l’attribut`data-icon-px-size`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. Si le lien partagé nécessite une authentification utilisateur et que l’aperçu d’URL de votre lien à partager ne s’affiche pas correctement dans Teams, vous pouvez désactiver l’aperçu de l’URL en ajoutant l’attribut `data-preview` défini sur `false`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si votre page affiche dynamiquement du contenu, vous pouvez utiliser la `shareToMicrosoftTeams.renderButtons()` méthode pour forcer **Share** à s’afficher à l’emplacement approprié dans le pipeline.

## <a name="craft-your-website-preview"></a>Créer la préversion de votre site web

Lorsque votre site web est partagé à Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web. Vous pouvez contrôler le comportement de cette préversion en vous assurant que les métadonnées appropriées sont ajoutées au site web en cours de partage, comme l’URL `data-href` .  

Pour afficher la préversion :

* Vous devez inclure une **image miniature** ou un **titre** et une **description**. Pour de meilleurs résultats, incluez les trois.
* L’URL partagée ne nécessite pas d’authentification. Si elle nécessite une authentification, vous pouvez la partager, mais la préversion n’est pas créée.

Le tableau suivant présente les balises nécessaires :

|Valeur|Balise META| Ouvrir Graph|
|----|----|----|
|Titre|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| Aucun. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Vous pouvez utiliser les versions HTML par défaut ou la version Open Graph.

## <a name="share-to-teams-for-education"></a>Partager vers Teams pour l'éducation

Pour les enseignants qui utilisent le bouton Partager pour Teams, il existe une option supplémentaire pour `Create an Assignment`. Cela vous permet de créer rapidement une affectation dans l’équipe choisie, en fonction du lien partagé. L’image suivante affiche Share to Teams for education :

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Partager vers Teams éducation contextuelle":::

## <a name="full-launcherjs-definition"></a>Définition de launcher.js complète

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | Boolean (sous forme de chaîne) | `true` | Indique s’il faut afficher ou non un aperçu du contenu à partager. |
| iconPxSize | `data-icon-px-size` | number (sous forme de chaîne) | `32` | Taille en pixels du bouton Partager vers Teams à afficher. |
| msgText | `data-msg-text` | string | s/o | Texte par défaut à insérer avant le lien dans la zone de composition du message. Le nombre maximal de caractères est de 200. |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ « Instructions » des affectations. Le nombre maximal de caractères est de 200. |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ « Titre » des affectations. Le nombre maximal de caractères est de 50. |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (facultatif) : `{ elements?: HTMLElement[] }`

Actuellement, tous les boutons de partage sont affichés sur la page. Si un objet facultatif `options` est fourni avec une liste d’éléments, ces éléments sont rendus dans des boutons de partage.

### <a name="set-default-form-values"></a>Définir les valeurs de formulaire par défaut

Vous pouvez choisir de définir les valeurs par défaut des champs suivants sur le partage pour Teams formulaire :

* Dites quelque chose à ce sujet : `msgText`
* Instructions d’affectation : `assignInstr`
* Titre de l’affectation : `assignTitle`

#### <a name="example"></a>Exemple

 Les valeurs de formulaire par défaut sont fournies dans l’exemple suivant :

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>Voir aussi

* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
* [Partager vers Teams à partir d’une application ou d’un onglet personnel](share-to-teams-from-personal-app-or-tab.md)
