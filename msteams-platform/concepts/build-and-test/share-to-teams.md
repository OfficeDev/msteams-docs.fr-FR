---
title: Créer un bouton de partage Teams
description: Comment ajouter le bouton Share to Teams incorporé sur votre site web
ms.topic: reference
keywords: Partager Teams entre équipes
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014333"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a>Créer un bouton Partager vers Teams sur votre site web

>[!NOTE]
> * Seules les versions de bureau de Edge et Chrome sont pris en charge.
> * L’utilisation de freemium ou de comptes invités n’est pas prise en charge.

Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons Partager à Teams sur leurs pages web, ce qui lance l’expérience Partager avec Teams dans une fenêtre popup lorsque vous cliquez dessus. Cela vous permettra de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte.

![Fenêtre pop-up Partager avec Teams](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Comment incorporer un bouton Partager avec Teams

Tout d’abord, vous devez ajouter le `launcher.js` script sur votre page web.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

Ensuite, ajoutez un élément HTML sur votre page web avec l’attribut de classe et le lien `teams-share-button` à partager dans `data-href` l’attribut.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

Cela ajoute l’icône Microsoft Teams à votre site web.

![Icône Partager avec Teams](~/assets/icons/share-to-teams-icon.png)

Si vous le souhaitez, si vous souhaitez une taille d’icône différente pour le bouton Partager avec Teams, utilisez `data-icon-px-size` l’attribut.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Si vous savez que l’aperçu de l’URL à partir de votre lien à partager ne s’affichera pas bien dans Teams (par exemple, le lien nécessiterait l’authentification de l’utilisateur), vous pouvez désactiver l’aperçu de l’URL en ajoutant le jeu d’attributs à `data-preview` `false` .

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Si votre page restituera dynamiquement le contenu, vous pouvez utiliser la méthode pour forcer le bouton Partager à s’restituer à `shareToMicrosoftTeams.renderButtons()` l’endroit approprié dans le pipeline. 

## <a name="crafting-your-website-preview"></a>Création de l’aperçu de votre site web

Lorsque votre site web est partagé avec Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web. Vous pouvez contrôler le comportement de cet aperçu en vous assurant que les métadon données appropriées sont ajoutées au site web en cours de partage `data-href` (l’URL). Le tableau ci-dessous présente les balises nécessaires. Vous pouvez utiliser les versions html par défaut ou la version Open Graph.

Pour que l’aperçu s’affiche, vous devez :

* Incluez soit une image miniature, soit un titre et une description (pour obtenir de meilleurs résultats, incluez les trois).
* L’URL partagée ne peut pas nécessiter d’authentification. Si c’est le cas, vous pouvez toujours le partager, mais l’aperçu ne sera pas créé.

|Valeur|Balise META| Open Graph|
|----|----|----|
|Titre|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| aucune |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Partager avec Teams pour l’Éducation

Pour les enseignants qui utilisent le bouton Partager avec Teams, vous avez une option supplémentaire pour `Create an Assignment` . Cela vous permet de créer rapidement une affectation dans l’équipe sélectionnée en fonction du lien partagé.

![Fenêtre pop-up Partager avec Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Définition launcher.js complète

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | booléen (sous la mesure d’une chaîne) | `true` | Indique si un aperçu du contenu à partager est à afficher ou non. |
| iconPxSize | `data-icon-px-size` | number (en tant que chaîne) | `32` | Taille en pixels du bouton Partager avec Teams à restituer. |
| msgText | `data-msg-text` | string | s/o | Texte par défaut à insérer avant le lien dans la zone de composition du message (limite de 200 caractères) |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ d’affectations « Instructions » (limite de 200 caractères) |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ « Titre » des affectations (limite de 50 caractères) |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (facultatif) : `{ elements?: HTMLElement[] }`

Restituer tous les boutons de partage actuellement présents sur la page. Si un objet facultatif est fourni avec une liste d’éléments, ces éléments sont restituer dans `options` des boutons de partage.

### <a name="setting-default-form-values"></a>Définition des valeurs de formulaire par défaut

Si vous le souhaitez, vous pouvez choisir de définir des valeurs par défaut pour les champs suivants dans le formulaire Partager avec Teams :

* Dites quelque chose à ce sujet ( `msgText` )
* Instructions d’affectation ( `assignInstr` )
* Titre de l’affectation ( `assignTitle` )

#### <a name="example-default-form-values"></a>Exemple : valeurs de formulaire par défaut

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
