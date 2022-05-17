---
title: Partager vers Teams à partir d’applications web
description: Découvrez comment ajouter le bouton Partager dans Teams incorporé sur votre site web, avec un aperçu du site web, à l’aide d’exemples de code
ms.topic: reference
ms.localizationpriority: medium
keywords: Partager Teams – Partager dans Teams
ms.openlocfilehash: b3efd268e2bded3955c2d9ab76d6dea755d06b5a
ms.sourcegitcommit: a3567e3e1a52b8e3cb2072b037f0e75bd0f12e58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2022
ms.locfileid: "65439299"
---
# <a name="share-to-teams-from-web-apps"></a>Partager vers Teams à partir d’applications web

Les sites web tiers peuvent utiliser le script du lanceur pour incorporer des boutons Partager dans Teams sur leurs pages web. Lorsque vous sélectionnez, il lance l’expérience Partager vers Teams dans une fenêtre contextuelle. Cela vous permet de partager un lien directement vers n’importe quelle personne ou Microsoft Teams canal sans changer de contexte. Ce document vous guide dans la création et l’incorporation d’un bouton Partager dans Teams pour votre site web, créer la préversion de votre site web et étendre Partager dans Teams pour l'éducation.

> [!NOTE]
>
> * Seules les versions de bureau de Microsoft&nbsp;Edge et Google Chrome sont prises en charge.
> * L’utilisation de Freemium ou de comptes invités n’est pas prise en charge.  

L’image suivante affiche l’expérience contextuelle Partager dans Teams :

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Fenêtre contextuelle Partager avec Teams":::

## <a name="embed-a-share-to-teams-button"></a>Incorporer bouton Partage dans Teams

1. Ajoutez le script `launcher.js` sur votre page web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Ajoutez un élément HTML sur votre page web avec l’attribut de classe `teams-share-button` et le lien à partager dans l’attribut `data-href` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Une fois cette opération terminée, l’icône Microsoft Teams est ajoutée à votre site web. L’image suivante montre l’icône Partager dans Teams :

    ![Icône Partager dans Teams](~/assets/icons/share-to-teams-icon.png)

1. Sinon, si vous souhaitez une taille d’icône différente pour le bouton Partager dans Teams, utilisez l’attribut`data-icon-px-size`.

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

1. Pour afficher un message de votre choix dans la zone de composition, vous pouvez définir votre texte dans l’attribut `data-msg-text` .

     ```html
     <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-msg-text="<default-message-to-be-populated-in-compose-box>"
      data-preview="false">
      </div>
     ```

1. Si votre page affiche dynamiquement du contenu, vous pouvez utiliser la `shareToMicrosoftTeams.renderButtons()` méthode pour forcer **Partager** à s’afficher à l’emplacement approprié dans le pipeline.

## <a name="craft-your-website-preview"></a>Créer la préversion de votre site web

Lorsque votre site web est partagé dans Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web. Vous pouvez contrôler le comportement de cette préversion en vous assurant que les métadonnées appropriées sont ajoutées au site web en cours de partage, comme l’URL `data-href` .  

Pour afficher l’aperçu :

* Vous devez inclure une **image miniature** ou un **titre** et une **Description**. Pour de meilleurs résultats, incluez les trois.
* L’URL partagée ne nécessite pas d’authentification. Si elle nécessite une authentification, vous pouvez la partager, mais la préversion n’est pas créée.

Le tableau suivant présente les balises nécessaires :

|Valeur|Balise META| Open Graph|
|----|----|----|
|Titre|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| aucun. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Vous pouvez utiliser les versions HTML par défaut ou la version Open Graph.

## <a name="share-to-teams-for-education"></a>Partager dans Teams pour l’Éducation

Pour les enseignants qui utilisent le bouton Partager dans Teams, il existe une option supplémentaire pour `Create an Assignment`. Cela vous permet de créer rapidement une affectation dans l’équipe choisie, en fonction du lien partagé. L’image suivante affiche Partager dans Teams pour l’Éducation :

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Éducation contextuelle Partager dans Teams":::

## <a name="full-launcherjs-definition"></a>Définition de launcher.js complète

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | Boolean (sous forme de chaîne) | `true` | Indique s’il faut afficher ou non un aperçu du contenu à partager. |
| iconPxSize | `data-icon-px-size` | nombre (sous forme de chaîne) | `32` | Taille en pixels du bouton Partager dans Teams à afficher. |
| msgText | `data-msg-text` | chaîne | s/o | Texte par défaut à insérer avant le lien dans la zone de rédaction du message. Le nombre maximal de caractères est de 200. |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ « Instructions » des devoirs. Le nombre maximal de caractères est de 200. |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ « Titre » des devoirs. Le nombre maximal de caractères est de 50. |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (facultatif) : `{ elements?: HTMLElement[] }`

Actuellement, tous les boutons de partage sont affichés sur la page. Si un objet facultatif `options` est fourni avec une liste d’éléments, ces éléments sont rendus dans des boutons de partage.

### <a name="set-default-form-values"></a>Définir les valeurs de formulaire par défaut

Vous pouvez choisir de définir les valeurs par défaut des champs suivants sur le formulaire Partager dans Teams :

* Écrivez un commentaire : `msgText`
* Instructions de devoir : `assignInstr`
* Titre du devoir : `assignTitle`

#### <a name="example"></a>Exemple

 Les valeurs de formulaire par défaut sont fournies dans l’exemple suivant :

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
* [Partager dans Teams à partir d’une application ou d’un onglet personnel](share-to-teams-from-personal-app-or-tab.md)
