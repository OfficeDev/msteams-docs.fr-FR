---
title: Créez un canal personnalisé et un onglet de groupe avec Node.js et le générateur Yeoman pour Microsoft Teams
author: laujan
description: Un guide quickstart pour créer un canal et un onglet de groupe avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566643"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Créez un canal personnalisé et un onglet de groupe à l’aide Node.js et du générateur Yeoman pour Microsoft Teams

>[!NOTE]
>Ce quickstart suit les étapes décrites dans [le Wiki Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) trouvé dans le référentiel microsoft OfficeDev GitHub’ordinateur.

Dans ce quickstart nous allons walk-through créer un canal personnalisé et onglet de groupe en [utilisant le Teams générateur Yeoman](https://github.com/OfficeDev/generator-teams/).

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Voulez-vous créer un onglet configurable ou statique ?**

Utilisez les touches fléchées pour sélectionner l’onglet configurable.

**Quelles étendues avez-vous l’intention d’utiliser pour votre onglet ?**

Vous pouvez sélectionner une équipe et/ou un chat de groupe

**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (Y/n)** 

Sélectionnez **n**.

>[!IMPORTANT]
>Le composant de **chemin yourDefaultTabNameTab**, référencé dans ce quickstart, est la valeur que vous avez entré dans le générateur pour **nom d’onglet par** défaut plus le mot **Onglet**.
>
>Par exemple: DefaultTabName: **MyTab**  =>  **/MyTabTab/**

Dans votre répertoire de projet, accédez aux éléments suivants :

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

C’est là que vous trouverez votre logique onglet. `render()`Localisez la méthode et ajoutez la balise et le contenu suivants en haut du code de `<div>` conteneur `<PanelBody>` :

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Assurez-vous d’enregistrer le fichier mis à jour.

## <a name="build-and-run-your-application"></a>Créez et exécutez votre application

Ouvrez une invite de commande dans votre répertoire de projet pour accomplir les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour afficher votre page de configuration d’onglet, rendez-vous `https://localhost:3007/<yourDefaultAppNameTab>/config.html` sur . Vous devez voir les éléments ci-après :

![capture d’écran de page de configuration](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établissez un tunnel sécurisé à votre onglet

Microsoft Teams est un produit entièrement basé sur le cloud et exige que le contenu de votre onglet soit disponible à partir du cloud à l’aide des paramètres HTTPS. Teams n’autorise pas l’hébergement local, par conséquent, vous devez soit publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL orientée vers Internet.

Pour tester votre extension d’onglet, vous [utiliserez ngrok](https://ngrok.com/docs), qui est intégré dans cette application. Ngrok est un outil logiciel proxy inversé qui créera un tunnel vers les points de terminaison HTTPS accessibles au public de votre serveur Web en cours d’exécution locale. Les paramètres Web de votre serveur seront disponibles pendant la session en cours sur votre machine locale. Lorsque la machine est arrêtée ou s’enort, le service ne sera plus disponible.

Dans votre invite de commande, sortez localhost et entrez ce qui suit :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé sur les équipes Microsoft et enregistré avec succès, vous pouvez le voir dans la galerie d’onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session tunnel ngrok. Si vous redémarrez votre session ngrok, vous devrez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-application-to-teams"></a>Télécharger votre demande à Teams

- Ouvrez le Microsoft Teams client. Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).
- Dans le *panneau YourTeams* à gauche, sélectionnez le `...` menu à côté de l’équipe que vous utilisez pour tester votre onglet et choisir **l’équipe Manage**.
- Dans le panneau principal, **sélectionnez Apps** à partir de la barre d’onglet **et choisissez Télécharger une application** personnalisée située dans le coin inférieur droit de la page.
- Ouvrez votre répertoire de projet, naviguez sur le **dossier ./package,** sélectionnez le dossier zip du paquet d’application et choisissez **Open**. Votre onglet sera téléchargé dans Teams.
- Retournez dans votre équipe, choisissez le canal où vous souhaitez afficher l’onglet, sélectionnez ➕ de la barre d’onglets et choisissez votre onglet dans la galerie.
- Suivez les instructions pour ajouter un onglet. Notez qu’il existe un dialogue de configuration personnalisé pour votre onglet canal/groupe.
- Sélectionnez **Enregistrer** et votre onglet sera ajouté à la barre d’onglets du canal.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créez un onglet Canal personnalisé et groupe avec ASP.NETCore](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)