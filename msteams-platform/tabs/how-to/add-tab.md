---
title: Étendre votre application teams avec un onglet personnalisé
author: laujan
description: Guide de création d’un onglet
keywords: onglet teams groupe de canaux configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 0434aabc39900e8f8232ae307a5854b2eb3a756d
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819031"
---
# <a name="extend-your-teams-app-with-a-custom-tab"></a>Étendre votre application teams avec un onglet personnalisé

Les onglets personnalisés vous permettent de prendre en charge le contenu Web que vous hébergez sur votre canal, la conversation de groupe et les utilisateurs personnels. À un niveau élevé, vous devez effectuer les étapes suivantes pour créer un onglet :

1. Préparez votre environnement de développement.
1. Créez vos pages.
1. Hébergez votre service d’application.
1. Créez votre package d’application et téléchargez-le dans Microsoft Teams.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-pages"></a>Créer vos pages

Que vous présentiez votre onglet au sein de l’étendue personnelle ou de la chaîne/du groupe, il se compose d’une ou de plusieurs pages HTML que vous hébergez. Les onglets avec une étendue personnelle se composent d’une seule page de contenu, tandis que les onglets avec un canal ou une étendue de groupe nécessitent une page de configuration qui définit l’URL de la page de contenu en fonction de l’entrée de l’utilisateur au moment de l’installation.

Il existe trois types de pages d’onglets. Consultez la page de documentation correspondante pour obtenir des informations complètes sur leur création.

1. [Page de contenu](~/tabs/how-to/create-tab-pages/content-page.md), page affichée dans un onglet.
1. [Page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md), page utilisée pour définir ou mettre à jour l’URL de la page de contenu, et l’ajouter à un onglet canal/groupe.
1. [Page de suppression](~/tabs/how-to/create-tab-pages/removal-page.md), page facultative qui s’affiche lorsqu’un onglet de canal/groupe est supprimé.

### <a name="tab-requirements"></a>Conditions requises par les onglets

Quel que soit le type de page, vous devez respecter les conditions suivantes :

* Vous devez autoriser le renvoi de vos pages dans un IFrame, via les en-têtes X-Frame-options et/ou Content-Security-Policy.
  * En-tête Set : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`        
  * Pour la compatibilité avec Internet Explorer 11, définissez-la `X-Content-Security-Policy` également.    
  * Vous pouvez également définir en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Cet en-tête est déconseillé, mais il est toujours respecté par la plupart des navigateurs.
* En règle générale, comme protection contre les prises de rendez-vous, les pages de connexion ne s’affichent pas dans les IFrames. Par conséquent, votre logique d’authentification doit utiliser une méthode autre que Redirect (par exemple, utiliser l’authentification basée sur des jetons ou une authentification par cookie).

> [!NOTE]
> Chrome 80, planifié pour la publication au début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies au lieu de vous appuyer sur le comportement par défaut du navigateur. *Voir* [SameSite cookie Attribute (mise à jour 2020)](../../resources/samesite-cookie-update.md).

* Les navigateurs adhèrent à une restriction de stratégie de même origine qui empêche une page Web d’effectuer des demandes à un domaine différent de celui qui a servi à une page Web. Toutefois, vous devrez peut-être rediriger la configuration ou la page de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation inter-domaines doit permettre au client teams de valider l’origine par rapport à une liste validDomains statique dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Pour créer une expérience transparente, vous devez appliquer un style à vos onglets en fonction du thème, de la conception et de l’intention du client Teams. En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus afin de répondre à un besoin spécifique et de se concentrer sur un petit ensemble de tâches ou sur un sous-ensemble de données correspondant à l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence au [Kit de développement logiciel (SDK) JavaScript du client Microsoft teams](/javascript/api/overview/msteams-client) à l’aide de balises script. À la suite de votre chargement de page, effectuez un appel à `microsoftTeams.initialize()` . Votre page ne s’affichera pas si vous ne le faites pas.

## <a name="host-your-app-service"></a>Héberger votre service d’application

Votre contenu doit être hébergé sur une URL disponible publiquement disponible à l’aide du protocole HTTPs. À des fins de test, vous pouvez utiliser un proxy inverse, tel que [ngrok](https://ngrok.com/), pour exposer votre port local à une URL accessible sur Internet.

## <a name="create-your-app-package-with-app-studio"></a>Créer votre package d’application avec App Studio

Vous pouvez utiliser l’application App Studio à partir du client Microsoft teams pour vous aider à créer votre manifeste d’application. Si vous n’avez pas installé App Studio dans Teams, **Sélectionnez** ![ application Store app dans ](/microsoftteams/platform/assets/images/tab-images/storeApp.png) le coin inférieur gauche de l’application Teams, puis recherchez App Studio. Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez installer dans la boîte de dialogue fenêtre contextuelle.

1. Ouvrir le client Microsoft teams : l’utilisation de la [version Web](https://teams.microsoft.com) vous permet d’inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.
1. Ouvrez l’application Studio et sélectionnez l’onglet **éditeur de manifeste** .
1. Sélectionnez la vignette **créer une nouvelle application** .
1. Ajoutez les détails de votre application (consultez la [définition de schéma de manifeste](~/resources/schema/manifest-schema.md) pour obtenir une description complète de chaque champ).
1. Dans la section fonctionnalités, sélectionnez **tabulations**.
    * Pour un onglet personnel, choisissez *Ajouter un onglet personnel* , puis sélectionnez **Ajouter**. Une fenêtre de boîte de dialogue contextuelle s’affiche, dans laquelle vous pouvez ajouter les détails de votre onglet.
    * Pour un onglet canal/groupe, sous l' *onglet équipe* , sélectionnez **Ajouter** et renseignez les champs de détails de l’onglet dans la fenêtre contextuelle de l’onglet équipe. Vérifier que la *mise à jour de la configuration est possible * Les zones de conversation d’équipe et de *groupe* sont cochées, puis sélectionnez **Enregistrer**.
1. Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL d’hôte ou de proxy inverse, sans le préfixe https.
1. À partir de l’onglet **Terminer**le  =>  **test et répartir** , vous pouvez **Télécharger** votre package d’application, **installer** le package dans une équipe ou l' **Envoyer** au magasin d’applications teams pour approbation. *Si vous utilisez un proxy inverse, vous obtiendrez un avertissement dans le **champ Description** à droite. L’avertissement peut être ignoré lors du test de votre onglet*.

## <a name="create-your-app-package-manually"></a>Créer manuellement votre package de l’application

Comme avec les robots et les extensions de messagerie, vous mettez à jour le [manifeste d’application](~/resources/schema/manifest-schema.md) de votre application pour inclure les propriétés de l’onglet. Ces propriétés régissent les étendues disponibles dans votre onglet, les URL à utiliser et diverses autres propriétés.

### <a name="personal-tabs"></a>Onglets personnels

Le contenu affiché pour les onglets personnels est le même pour tous les utilisateurs et est configuré dans le `staticTabs` groupe. Vous pouvez déclarer jusqu’à seize onglets personnels (16) dans une application.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`entityId`|String|64 caractères|✔|Identificateur unique de l’entité que l’onglet affiche.|
|`name`|Chaîne|128 caractères|✔|Nom d’affichage de l’onglet dans l’interface de canal.|
|`contentUrl`|Chaîne|2 048 caractères|✔|URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.|
|`websiteUrl`|Chaîne|2 048 caractères||URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.|
|`scopes`|Tableau de l’énum|1 |✔|Les onglets statiques prennent en charge uniquement l' `personal` étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre d’une application personnelle.|

#### <a name="simple-personal-tab-manifest-example"></a>Exemple de manifeste d’onglet personnel simple

L’exemple ci-dessous montre uniquement le `staticTabs` tableau d’un manifeste de l’application.

```json
...
"staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name for tab",
      "contentUrl": "https:// yourURL.com/content ",
      "websiteUrl": "https://yourURL.com/website",
      "scopes": [ "personal" ]
    }
...
```

### <a name="channelgroup-tabs"></a>Onglets canal/groupe

Les onglets canal/groupe sont ajoutés dans le `configurableTabs` tableau. Vous ne pouvez déclarer qu’un seul onglet canal/groupe dans le `configurableTabs` tableau.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`configurationUrl`|Chaîne|2 048 caractères|✔|URL https://vers la page de configuration.|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Default `true`|
|`scopes`|Tableau de l’énum|1 |✔|Les onglets configurables prennent en charge uniquement les `team` `groupchat` étendues et. |

#### <a name="simple-channelgroup-tab-manifest-example"></a>Exemple de manifeste de l’onglet canal/groupe simple

L’exemple ci-dessous montre uniquement le `configurableTabs` tableau d’un manifeste de l’application.

```json
...
"configurableTabs": [
    {
      "configurationUrl": "https://yourURL.com/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
...
```

Une fois que vous avez effectué le `manifest.json` regroupement dans un dossier zip avec vos deux icônes requises.

### <a name="upload-app-package-directly-to-a-team"></a>Télécharger un package d’application directement dans une équipe

1. Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.
1. Dans le volet *YourTeams* à gauche, sélectionnez le `...` menu en regard de l’équipe que vous utilisez pour tester votre onglet, puis sélectionnez **gérer l’équipe**.
1. Dans le panneau principal, sélectionnez **applications** dans la barre d’onglets et choisissez **Télécharger une application personnalisée** située dans l’angle inférieur droit de la page.
1. Ouvrez le répertoire de votre projet, accédez au dossier **./Package** , sélectionnez le dossier zip du package d’application, puis choisissez **ouvrir**. Votre onglet est chargé dans Teams.

### <a name="view-your-tab-in-teams"></a>Afficher votre onglet dans teams

1. Affichez votre onglet personnel :
    * Dans la barre de navigation située à l’extrême gauche du client Teams, sélectionnez le `...` menu et choisissez votre application dans la liste.

1. Affichez l’onglet canal/groupe :
    * Revenez à votre équipe, choisissez le canal où vous souhaitez afficher l’onglet, sélectionnez ➕ dans la barre d’onglets, puis choisissez votre onglet dans la Galerie.
    * Suivez les instructions relatives à l’ajout d’un onglet. Notez qu’il existe une boîte de dialogue de configuration personnalisée pour l’onglet canal/groupe. Sélectionnez **Enregistrer** et votre onglet est ajouté à la barre d’onglets de la chaîne.

## <a name="learn-more"></a>En savoir plus

* [Créer une page de contenu pour votre onglet](~/tabs/how-to/create-tab-pages/content-page.md)
* [Créer une page de configuration pour votre onglet](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Mettre à jour ou supprimer un onglet](~/tabs/how-to/create-tab-pages/removal-page.md)
