## <a name="create-the-app-package"></a>Créer le package d’application

Vous aurez besoin d’un package d’application pour tester votre onglet dans Teams. Il s’agit d’un dossier zip contenant les fichiers requis suivants :

- Une **icône de couleur complète** mesurant 192 x 192 pixels.
- **Icône de contour transparent** mesurant 32 x 32 pixels.
- Un fichier **Manifest. JSON** qui spécifie les attributs de votre application.

Le package est créé via une tâche Gulp qui valide le fichier manifest. JSON et génère le dossier zip dans le `./package directory`. Dans l’invite de commandes, entrez :

```bash
gulp manifest
```

## <a name="build-your-application"></a>Créer votre application

La commande de génération compile votre solution dans le dossier *. dossier/dist.* . Ensuite, entrez :

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>Exécuter votre application dans localhost

Démarrez un serveur Web local en entrant la commande suivante :

```bash
gulp serve
```

Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur et affichez la page d’accueil de votre application :

![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)