## <a name="create-the-app-package"></a><span data-ttu-id="f5aed-101">Créer le package d’application</span><span class="sxs-lookup"><span data-stu-id="f5aed-101">Create the app package</span></span>

<span data-ttu-id="f5aed-102">Vous aurez besoin d’un package d’application pour tester votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f5aed-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="f5aed-103">Il s’agit d’un dossier zip qui contient les fichiers requis suivants :</span><span class="sxs-lookup"><span data-stu-id="f5aed-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="f5aed-104">Icône **en couleurs complètes** de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="f5aed-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="f5aed-105">Icône **de plan transparente de** 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="f5aed-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="f5aed-106">Un **manifest.jssur** le fichier qui spécifie les attributs de votre application.</span><span class="sxs-lookup"><span data-stu-id="f5aed-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="f5aed-107">Le package est créé via une tâche Gulp qui valide la manifest.jssur le fichier et génère le dossier zip dans `./package directory` le fichier .</span><span class="sxs-lookup"><span data-stu-id="f5aed-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="f5aed-108">Dans l’invite de commandes, entrez :</span><span class="sxs-lookup"><span data-stu-id="f5aed-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="f5aed-109">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="f5aed-109">Build your application</span></span>

<span data-ttu-id="f5aed-110">La commande de build transpile votre solution dans le *dossier ./dist.*</span><span class="sxs-lookup"><span data-stu-id="f5aed-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="f5aed-111">Ensuite, entrez :</span><span class="sxs-lookup"><span data-stu-id="f5aed-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="f5aed-112">Exécuter votre application dans localhost</span><span class="sxs-lookup"><span data-stu-id="f5aed-112">Run your application in localhost</span></span>

<span data-ttu-id="f5aed-113">Démarrez un serveur web local en entrant les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5aed-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="f5aed-114">Entrez `http://localhost:3007/<yourDefaultAppNameTab>/` dans votre navigateur et affichez la page d’accueil de votre application :</span><span class="sxs-lookup"><span data-stu-id="f5aed-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![capture d’écran de la page d’accueil](~/assets/images/tab-images/homePage.png)