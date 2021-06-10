---
title: Créez un onglet de groupe et de canal personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet de canal et de groupe avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 70b1dbe5a5abafa44ddbdf9045c55a33cf8fcb20
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630238"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Créer un canal et un onglet de groupe personnalisés à l’aide Node.js et du générateur Yeoman pour Microsoft Teams

>[!NOTE]
>Ce démarrage rapide suit les étapes décrites dans le [Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) de votre première application Microsoft Teams dans le référentiel d’GitHub Microsoft OfficeDev.

Dans ce démarrage rapide, nous allons créer un canal et un onglet de groupe personnalisés à l’aide Teams [générateur Yeoman.](https://github.com/OfficeDev/generator-teams/)

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Voulez-vous créer un onglet configurable ou statique ?**

Utilisez les touches de direction pour sélectionner un onglet configurable.

**Quelles étendues avez-vous l’intention d’utiliser pour votre onglet ?**

Vous pouvez sélectionner une équipe et/ou une conversation de groupe

**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (Y/n)** 

Sélectionnez **n**.

>[!IMPORTANT]
>The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.
>
>Par exemple : DefaultTabName: **MyTab**  =>  **/MyTabTab/**

Dans le répertoire de votre projet, accédez à ce qui suit :

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

C’est là que se trouve la logique de votre onglet. Recherchez la méthode et ajoutez la balise et le contenu suivants `render()` en haut du code de conteneur `<div>` `<PanelBody>` :

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Veillez à enregistrer le fichier mis à jour.

## <a name="build-and-run-your-application"></a>Créer et exécuter votre application

Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour afficher la page de configuration de votre onglet, allez à `https://localhost:3007/<yourDefaultAppNameTab>/config.html` . Vous devez voir les éléments ci-après :

![capture d’écran de la page de configuration](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft Teams est un produit entièrement basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local, par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL internet.

Pour tester votre extension d’onglet, vous allez utiliser [ngrok,](https://ngrok.com/docs)qui est intégré à cette application. Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Les points de terminaison web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local. Lorsque l’ordinateur est arrêté ou mis en veille, le service n’est plus disponible.

Dans votre invite de commandes, quittez localhost et entrez les commandes suivantes :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé vers Microsoft Teams et enregistré, vous pouvez l’afficher dans la galerie d’onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session tunnel ngrok. Si vous redémarrez votre session ngrok, vous devez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

- Ouvrez le client Microsoft Teams client. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils [de développement de votre navigateur.](~/tabs/how-to/developer-tools.md)
- Dans le *panneau YourTeams* sur la gauche, sélectionnez le menu en face de l’équipe que vous utilisez pour tester votre onglet et choisissez `...` Gérer **l’équipe.**
- Dans le panneau principal, sélectionnez **Applications** dans la barre d’onglets et **choisissez Télécharger** une application personnalisée située dans le coin inférieur droit de la page.
- Ouvrez le répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip du package d’application et choisissez **Ouvrir.** Votre onglet est chargé dans Teams.
- Revenir à votre équipe, choisissez le canal dans lequel vous souhaitez afficher l’onglet, sélectionnez ➕ dans la barre d’onglets et choisissez votre onglet dans la galerie.
- Suivez les instructions pour ajouter un onglet. Notez qu’il existe une boîte de dialogue de configuration personnalisée pour votre onglet canal/groupe.
- Sélectionnez **Enregistrer** et votre onglet sera ajouté à la barre d’onglets du canal.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet canal et de groupe personnalisé avec ASP.NETCore](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
