---
title: Didacticiel - Créer votre première application à l’aide du générateur Yeoman
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566823"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Créer votre première application Microsoft Teams à l’aide du générateur Yeoman

> [!Note]
> Ce didacticiel provient du [générateur Yeoman pour Teams wiki.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

Dans ce didacticiel, nous allons parcourir la création de votre toute première application Microsoft Teams l’aide Microsoft Teams générateur Yeoman. Il vous permet également de passer par le processus de mise à niveau de votre Teams à l’aide du générateur Yeoman. La condition préalable pour commencer avec ce didacticiel est que vous avez un compte Teams qui permet le chargement de version de version [d’application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Installer et préparer votre ordinateur

Vous devez installer ce qui suit sur votre ordinateur avant de commencer à utiliser le générateur Yeoman.

### <a name="install-nodejs"></a>Installer Node.js.

Vous devez avoir installé Node.js sur votre ordinateur. Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)

### <a name="install-a-code-editor"></a>Installer un éditeur de code

Vous avez besoin d’un éditeur de code. La plupart de cette documentation et des images font référence à l’utilisation [Visual Studio Code](https://code.visualstudio.com). Toutefois, n’hésitez pas à utiliser l’éditeur de texte de votre choix.

### <a name="install-yeoman-and-gulp-cli"></a>Installer Yeoman et Gulp CLI

Pour échafauder des projets à l’aide du générateur, vous devez installer l’outil Yeoman et le gestionnaire des tâches gulp CLI.

Ouvrez une invite de commandes et tapez ce qui suit :

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>Installer le générateur

Installez le Teams générateur Yeoman avec la commande suivante :

```bash
npm install generator-teams --global
```

Installez la version d’aperçu du générateur avec la commande suivante :

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Générer votre projet

Cette section vous présente les étapes de génération de votre projet.

**Pour générer votre projet**

1. Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet, puis exécutez la commande dans ce `yo teams` répertoire. Le générateur démarre.
1. Répondez à l’ensemble des questions posées par le générateur :

   ![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

   1. La première question porte sur le nom de votre projet, vous pouvez le laisser tel qu’il est en appuyant sur Entrée.
   1. La question suivante vous demande si vous souhaitez créer un répertoire ou utiliser le répertoire actuel. Comme vous êtes déjà dans le répertoire que vous souhaitez, appuyez simplement sur Entrée.
   1. Dans la question suivante, tapez le titre de votre projet. Ce titre sera utilisé dans le manifeste et la description de votre application. 
   1. Ensuite, un nom de société vous sera demandé, qui sera également utilisé dans le manifeste.
   1. La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser. Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.
   1. Ensuite, le générateur vous demandera quels éléments vous souhaitez ajouter à votre projet. Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments. Pour ce didacticiel, sélectionnez *simplement un onglet*:

    ![sélection d’élément](~/assets/yeoman-images/teams-first-app-2.png)

1. Répondez à l’ensemble suivant de questions de suivi qui s’affichent en fonction des éléments que vous avez sélectionnés à l’étape 2.
1. Entrez une URL de l’endroit où vous hébergez votre solution. 

   > [!NOTE]
   > L’URL peut être n’importe quelle URL, mais par défaut, le générateur suggère une URL de site web Azure.

1. Dans la question suivante, confirmez si vous souhaitez inclure des tests unitaires pour votre solution. La réponse par défaut est *oui*. Si vous choisissez d’inclure le test unitaire, le projet généré aura une infrastructure de test unitaire et certains tests unitaires par défaut pour les différents éléments en cours de structure. 
   > [!NOTE]
   > * Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.
   > * Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d’utiliser ou de refuser.

1. Pour faciliter la signature, vous serez également invité à utiliser Azure Application Insights pour la signature. Si vous choisissez *Oui,* vous devez fournir une clé Azure Application Insights. 

   > [!NOTE]
   > Pour ce didacticiel, dés optez pour l’utilisation d’Application Insights.

L’ensemble de questions suivant sera basé sur les éléments précédemment sélectionnés. Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d’utiliser cette application en tant que SharePoint Web Part Online. Une fois que vous avez fourni le nom, le générateur génère le projet et installe toutes les dépendances. Cela prendra une minute ou deux.

## <a name="add-some-code-to-your-tab"></a>Ajouter du code à votre onglet

Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori. Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé. Pour plus d’informations, [voir Project structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)

Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier. Il s’agit de la classe React TypeScript pour votre onglet. Recherchez la méthode et ajoutez une ligne de code à l’intérieur du contrôle afin `render()` `<PanelBody>` qu’elle ressemble à ceci :

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Enregistrez le fichier et revenir à l’invite de commandes.

## <a name="build-your-app"></a>Créer votre application

Vous pouvez maintenant créer votre projet. Cette étape est effectuée en deux étapes (ou une étape, voir ci-dessous).

Tout d’abord, vous devez créer le Teams manifeste de l’application, que vous chargez/chargez de Microsoft Teams. Cette tâche est effectuée par la tâche `gulp manifest` Gulp. Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.

Pour créer votre solution, utilisez la `gulp build` commande. Cela transpile votre solution dans le `./dist` dossier. 

## <a name="run-your-app"></a>Exécuter votre application

Pour exécuter votre application, utilisez la `gulp serve` commande. Cela permet de créer et de démarrer un serveur web local pour tester votre application. La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet. 

Vous devez maintenant être en mesure de parcourir pour `http://localhost:3007/myFirstAppTab/` vous assurer que votre onglet est rendu. Toutefois, pas encore Microsoft Teams :

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Exécuter votre application dans Microsoft Teams

Microsoft Teams ne vous permet pas d’héberger votre application sur localhost, vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok.

La bonne nouvelle est que le projet échafaudé dispose de ce pré-projet intégré. Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .

Après l’exécution, créez une équipe Microsoft Teams et, lorsqu’elle est créée, cliquez sur le nom de l’équipe, pour aller aux paramètres d’équipe, puis `gulp ngrok-serve` sélectionnez *Applications.* Dans le coin inférieur droit, vous devez voir un *lien Télécharger* une application personnalisée, sélectionnez-la, puis accédez au dossier de votre projet et au sous-dossier `package` appelé. Sélectionnez le fichier zip dans ce dossier, puis ouvrez. Votre application est désormais rechargée de Microsoft Teams :

![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

Revenir au canal *Général* et choisir *+* d’ajouter un nouvel onglet. Vous devez voir votre onglet dans la liste d’onglets :

![configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)

Choisissez votre onglet et suivez les instructions pour l’ajouter. Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source. Sélectionnez *Enregistrer* pour ajouter votre onglet au canal. Une fois que vous avez terminé, votre onglet doit être chargé dans Microsoft Teams !

![exécution de l’onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>Mise à niveau Microsoft Teams

Vous pouvez également mettre à niveau votre version Microsoft Teams actuelle vers la dernière version à l’aide Microsoft Teams générateur Yeoman.

**Pour mettre à niveau Microsoft Teams**

1. Obtenez la version actuelle de Teams avec la commande suivante :

   ```PowerShell
    yo teams --version
   ```
2. Utilisez la commande suivante pour sélectionner mettre à jour votre générateur :

   ```PowerShell
    yo
   ```
3. Utilisez les touches de direction pour choisir **Mettre à jour vos générateurs**:

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
   
**Félicitations ! Vous avez créé et déployé votre première application Microsoft Teams de messagerie. Vous avez également mis à niveau Microsoft Teams.**
