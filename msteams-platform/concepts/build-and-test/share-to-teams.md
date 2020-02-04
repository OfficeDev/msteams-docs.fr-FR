---
title: Bouton partager avec teams incorporés
description: Comment ajouter le bouton partager à teams incorporé sur votre site Web
keywords: Partager des équipes partager partage-équipe
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673886"
---
# <a name="creating-a-share-to-teams-embedded-button"></a>Création d’un bouton partager avec teams incorporés

>[!NOTE]
> * Seules les versions de bureau Edge et chrome sont prises en charge.
> * L’utilisation de comptes freemium ou invités n’est pas prise en charge.

Les sites Web tiers peuvent utiliser le script de lancement pour incorporer les boutons partager à teams sur leurs pages Web, ce qui lancera l’expérience de partage vers teams dans une fenêtre contextuelle lorsque vous cliquerez dessus. Cela vous permettra de partager un lien directement avec une personne ou un canal Microsoft teams sans basculer le contexte.

![Partager le menu contextuel teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Comment incorporer un bouton partager à teams

Tout d’abord, vous devez ajouter le `launcher.js` script sur votre page Web.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

Ensuite, ajoutez un élément HTML sur votre page Web avec `teams-share-button` l’attribut Class et le lien à partager dans `data-href` l’attribut.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

Cette opération ajoute l’icône Microsoft teams à votre site Web.

![Icône partager avec teams](~/assets/icons/share-to-teams-icon.png)

Éventuellement, si vous voulez une taille d’icône différente pour le bouton partager avec Teams, utilisez `data-icon-px-size` l’attribut.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Si vous êtes certain que l’aperçu de l’URL de votre lien à partager ne s’affiche pas correctement dans Teams (par exemple, le lien nécessite l’authentification de l’utilisateur), `data-preview` vous pouvez désactiver `false`l’aperçu de l’URL en ajoutant l’attribut défini à.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Si votre page affiche le contenu de manière dynamique, vous pouvez utiliser la `shareToMicrosoftTeams.renderButtons()` méthode pour forcer le rendu du bouton **partager** à l’emplacement approprié dans le pipeline.

## <a name="crafting-your-website-preview"></a>Conception de l’aperçu de votre site Web

Lorsque votre site Web est partagé avec Teams, la carte insérée dans la chaîne sélectionnée contiendra un aperçu de votre site Web. Vous pouvez contrôler le comportement de cet aperçu en veillant à ce que les méta-données appropriées soient ajoutées au site Web partagé `data-href` (URL). Le tableau suivant présente les balises nécessaires. Vous pouvez utiliser les versions par défaut de HTML ou la version d’Open Graph.

Pour afficher l’aperçu, vous devez :

* Inclure une image miniature, ou les deux, un titre et une description (pour de meilleurs résultats, incluez les trois).
* L’URL partagée ne peut pas exiger l’authentification. Si c’est le cas, vous pouvez toujours le partager, mais l’aperçu n’est pas créé.

|Valeur|Balise META| Ouvrir un graphique|
|----|----|----|
|Titre|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| none |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Partager avec teams pour l’éducation

Pour les enseignants qui utilisent le bouton partager avec teams `Create an Assignment`, une option supplémentaire est proposée. Cela vous permet de créer rapidement une affectation dans l’équipe choisie en fonction du lien partagé.

![Partager le menu contextuel teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Définition complète du lanceur. js

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | Boolean (sous forme de chaîne) | `true` | Indique si un aperçu du contenu à partager doit être affiché ou non. |
| iconPxSize | `data-icon-px-size` | nombre (sous forme de chaîne) | `32` | Taille en pixels du bouton partager-à-teams à afficher. |
| msgText | `data-msg-text` | string | s/o | Texte par défaut à insérer avant le lien dans la zone de composition du message (200 caractères maximum) |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ « instructions » des affectations (200 caractères maximum) |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ affectations « title » (50 caractères maximum) |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`(facultatif) :`{ elements?: HTMLElement[] }`

Affiche tous les boutons de partage actuellement sur la page. Si un objet `options` facultatif est fourni avec une liste d’éléments, ces éléments seront rendus dans les boutons de partage.

### <a name="setting-default-form-values"></a>Définition des valeurs de formulaire par défaut

Vous pouvez également définir des valeurs par défaut pour les champs suivants dans le formulaire partager avec teams :

* Signification de ce (`msgText`)
* Instructions d’affectation`assignInstr`()
* Titre de l'`assignTitle`affectation ()

#### <a name="example-default-form-values"></a>Exemple : valeurs de formulaire par défaut

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
