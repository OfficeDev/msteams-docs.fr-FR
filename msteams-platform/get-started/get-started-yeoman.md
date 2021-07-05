---
title: Didacticiel - Créer votre première application à l’aide du générateur Yeoman
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: a3519da1495dc51a811f4e95bc4ada9b11aa8292
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254342"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Créer votre première application Microsoft Teams à l’aide du générateur Yeoman

> [!Note]
> Ce didacticiel provient du [générateur Yeoman pour Teams wiki.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

Dans ce didacticiel, vous allez apprendre à créer votre toute première application Microsoft Teams à l’aide Microsoft Teams générateur Yeoman. Il vous permet également de passer par le processus de mise à niveau de votre Teams à l’aide du générateur Yeoman. Avant de commencer, vous devez avoir un compte Teams qui autorise le chargement de version de version [d’application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Vous devez installer les logiciels suivants sur votre ordinateur avant de commencer à utiliser le générateur Yeoman :

* Node.js

   Vous devez avoir installé Node.js sur votre ordinateur. Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)

* Un éditeur de code

   Vous avez besoin d’un éditeur de code. La plupart de cette documentation et des images font référence à l’utilisation [Visual Studio Code](https://code.visualstudio.com). Toutefois, n’hésitez pas à utiliser l’éditeur de texte de votre choix.

* Yeoman et Gulp CLI

   Pour échafauder des projets à l’aide du générateur, vous devez installer l’outil Yeoman et le gestionnaire des tâches gulp CLI.

   Ouvrez une invite de commandes et tapez ce qui suit :

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a>Installer le générateur

Installez le Teams générateur Yeoman avec la commande suivante :

```bash
npm init yo teams
```

Installez la version d’aperçu du générateur avec la commande suivante :

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a>Générer votre projet

Cette section vous présente les étapes à suivre pour générer votre projet.

**Pour générer votre projet**

1. Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet.
1. Go to the directory, and run the command `yo teams` . Le générateur démarre.
1. Répondez à l’ensemble des questions posées par le générateur :

   ![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

   1. Entrez un nom pour votre projet. Vous pouvez la laisser telle qu’elle est en appuyant sur Entrée.
   1. Entrez un chemin d’accès pour le nouveau répertoire si vous souhaitez créer un répertoire. Comme vous êtes déjà dans le répertoire de votre recherche, appuyez simplement sur Entrée.
   1. Entrez le titre de votre projet. Ce titre sera utilisé dans le manifeste et la description de votre application. 
   1. Entrez un nom de société qui sera également utilisé dans le manifeste.
   1. Entrez la version du manifeste que vous souhaitez utiliser. Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.
   1. Sélectionnez les éléments que vous souhaitez ajouter à votre projet. Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments. Pour ce didacticiel, sélectionnez *simplement un onglet*:

    ![sélection d’élément](~/assets/yeoman-images/teams-first-app-2.png)

1. Répondez à l’ensemble suivant de questions de suivi qui s’affichent en fonction des éléments que vous avez sélectionnés à l’étape 2.
1. Entrez une URL pour l’emplacement où vous hébergez votre solution. 

   > [!NOTE]
   > L’URL peut être n’importe quelle URL, mais par défaut, le générateur suggère une URL de site web Azure.

1. Confirmez si vous souhaitez inclure des tests unitaires pour votre solution. La réponse par défaut est **Oui**. Si vous choisissez d’inclure le test unitaire, le projet généré aura une infrastructure de test unitaire et certains tests unitaires par défaut pour les différents éléments en cours de structure. 
   > [!NOTE]
   > * Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.
   > * Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d’utiliser ou de refuser.

1. Pour faciliter la signature, vous serez également invité à utiliser Azure Application Informations pour la signature. Si vous **sélectionnez Oui,** vous devez fournir une clé d’Informations application Azure. 

   > [!NOTE]
   > Pour ce didacticiel, désinsévez l’utilisation d’Application Informations.

   L’ensemble de questions suivant sera basé sur les éléments précédemment sélectionnés. Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d’utiliser cette application en tant que SharePoint Web Part Online. Une fois que vous avez fourni le nom, le générateur génère le projet et installe toutes les dépendances. Cela prendra une minute ou deux.

## <a name="add-code-to-your-tab"></a>Ajouter du code à votre onglet

Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori. Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé. Pour plus d’informations, [voir Project structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)

Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier. Il s’agit de la classe React TypeScript pour votre onglet. 

1. Recherchez la méthode et ajoutez une ligne de code à l’intérieur du contrôle afin `render()` `<PanelBody>` qu’elle ressemble à ceci :

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. Enregistrez le fichier et revenir à l’invite de commandes.

## <a name="build-your-app"></a>Créer votre application

Vous pouvez maintenant créer votre projet. Cette procédure s’est effectuée en deux étapes.

1. Créez le Teams manifeste de l’application pour l’application que vous avez téléchargée dans Microsoft Teams. Cette tâche est effectuée par la tâche `gulp manifest` Gulp. Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.
1. Exécutez `gulp build` la commande pour créer la solution. Cela transpile votre solution dans le `./dist` dossier. 

## <a name="run-your-app"></a>Exécuter votre application

Pour exécuter votre application, utilisez la `gulp serve` commande. Cela permet de créer et de démarrer un serveur web local pour tester votre application. La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet. 

Vous devez maintenant vous assurer que votre `http://localhost:3007/myFirstAppTab/` onglet est rendu. Toutefois, il n’est pas Microsoft Teams pour le moment. 

**Pour restituer votre onglet dans Microsoft Teams**

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a>Exécuter votre application dans Microsoft Teams

Microsoft Teams ne vous permet pas d’héberger votre application sur localhost, vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok. La bonne nouvelle est que le projet échafaudé dispose de ce pré-projet intégré. 

**Pour exécuter votre application dans Teams**

1. `gulp ngrok-serve`S’exécute dans Terminal. Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .
1. Créez une équipe Microsoft Teams de recherche.
1. Sélectionnez le nom de l’équipe > Teams Paramètres > applications.
1. Dans le coin inférieur droit, **sélectionnez Télécharger une application personnalisée.**
1. Go to the `package` folder under your project folder. 
1. Sélectionnez le fichier zip dans ce dossier et sélectionnez Ouvrir. 
   Votre application est désormais rechargée de Microsoft Teams :

   ![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)
1. Revenir au canal **Général** et choisir **+** d’ajouter un nouvel onglet. Vous devez voir votre onglet dans la liste des onglets : ![ configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)
1. Sélectionnez votre onglet et suivez les instructions pour l’ajouter. Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source. Sélectionnez *Enregistrer* pour ajouter votre onglet au canal. Votre onglet est maintenant chargé à l’intérieur Microsoft Teams !

   ![exécution de l’onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a>Mise à niveau Microsoft Teams

Vous pouvez également mettre à niveau votre version Microsoft Teams actuelle vers la dernière version à l’aide Microsoft Teams générateur Yeoman.

**Pour mettre à niveau Microsoft Teams**

1. Obtenez la version actuelle de Teams avec la commande suivante :

   ```PowerShell
    yo teams --version
   ```
2. Utilisez la commande suivante pour sélectionner et mettre à jour votre générateur :

   ```PowerShell
    yo
   ```
3. Utilisez les touches de direction pour sélectionner **Mettre à jour vos générateurs**:

   ![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. Sélectionnez le générateur de votre choix dans la liste des générateurs :
   > [!NOTE]
   > Utilisez la barre d’espace pour sélectionner ou effacer une version Teams sélectionnée dans les options disponibles.

    ![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > L’installation de la Teams prend quelques secondes à quelques minutes.

5. Une fois l’installation terminée, utilisez la commande suivante pour vérifier la version installée :

   ```PowerShell
    yo teams --version
   ```
   Félicitations ! Vous avez créé et déployé votre première application Microsoft Teams de messagerie. Vous avez également mis à niveau Microsoft Teams.

 ## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)