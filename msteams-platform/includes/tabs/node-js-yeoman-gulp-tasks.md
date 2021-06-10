## <a name="create-the-app-package"></a>Créer le package d’application

Vous aurez besoin d’un package d’application pour tester votre onglet dans Teams. Il s’agit d’un dossier zip qui contient les fichiers requis suivants :

- Icône **en couleurs complètes** de 192 x 192 pixels.
- Icône **de plan transparente de** 32 x 32 pixels.
- Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.

Le package est créé via une tâche Gulp qui valide la manifest.jssur le fichier et génère le dossier zip dans `./package directory` le fichier . Dans l’invite de commandes, entrez :

```bash
gulp manifest
```

## <a name="build-your-application"></a>Créer votre application

La commande de build transpile votre solution dans le *dossier ./dist.* Ensuite, entrez :

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>Exécuter votre application dans localhost

Démarrez un serveur web local en entrant les données suivantes :

```bash
gulp serve
```

Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur et affichez la page d’accueil de votre application :

![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)