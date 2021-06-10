## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="5fd3d-101">Déployer votre application sur Azure</span><span class="sxs-lookup"><span data-stu-id="5fd3d-101">Deploy your app to Azure</span></span>

<span data-ttu-id="5fd3d-102">Le déploiement se compose de deux étapes.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-102">Deployment consists of two steps.</span></span>  <span data-ttu-id="5fd3d-103">Tout d’abord, les ressources cloud nécessaires sont créées (également appelées approvisionnement), puis le code qui constitue votre application est copié dans les ressources cloud créées.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-103">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="5fd3d-104">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5fd3d-104">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="5fd3d-105">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-105">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="5fd3d-106">Sélectionnez le Teams Shared Computer Toolkit la barre latérale en sélectionnant l’icône Teams côté.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-106">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="5fd3d-107">Sélectionnez **Provision dans le cloud**.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-107">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement":::

1. <span data-ttu-id="5fd3d-109">Si nécessaire, sélectionnez un abonnement à utiliser pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-109">If required, select a subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5fd3d-110">Certaines ressources Azure sont toujours utilisées pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-110">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="5fd3d-111">Une boîte de dialogue vous avertit que des coûts peuvent être encourus lors de l’exécution de ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-111">A dialog warns you that costs may be incurred when running resources in Azure.</span></span>  <span data-ttu-id="5fd3d-112">Appuyez **sur Provision**.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-112">Press **Provision**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="Capture d’écran de la boîte de dialogue d’approvisionnement.":::

   <span data-ttu-id="5fd3d-114">Le processus d’approvisionnement crée des ressources dans le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-114">The provisioning process will create resources in the Azure cloud.</span></span>  <span data-ttu-id="5fd3d-115">Cela prendra un certain temps.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-115">This will take some time.</span></span>  <span data-ttu-id="5fd3d-116">Vous pouvez surveiller la progression en regardant les boîtes de dialogue dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-116">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="5fd3d-117">Après quelques minutes, vous verrez l’avis suivant :</span><span class="sxs-lookup"><span data-stu-id="5fd3d-117">After a few minutes, you will see the following notice:</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée.":::

1. <span data-ttu-id="5fd3d-119">Une fois l’approvisionnement terminé, **sélectionnez Déployer dans le cloud.**</span><span class="sxs-lookup"><span data-stu-id="5fd3d-119">Once provisioning is complete, select **Deploy to the Cloud**.</span></span>  <span data-ttu-id="5fd3d-120">Comme pour l’approvisionnement, ce processus prend un certain temps.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-120">As with provisioning, this process takes some time.</span></span>  <span data-ttu-id="5fd3d-121">Vous pouvez surveiller le processus en regardant les boîtes de dialogue dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-121">You can monitor the process by watching the dialogs in the bottom right corner.</span></span> <span data-ttu-id="5fd3d-122">Après quelques minutes, vous verrez un avis d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-122">After a few minutes, you will see a completion notice.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="5fd3d-123">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="5fd3d-123">Command Line</span></span>](#tab/cli)

<span data-ttu-id="5fd3d-124">Dans la fenêtre de votre terminal :</span><span class="sxs-lookup"><span data-stu-id="5fd3d-124">In your terminal window:</span></span>

1. <span data-ttu-id="5fd3d-125">Exécutez `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-125">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="5fd3d-126">Vous pouvez être invité à vous connecter à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-126">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="5fd3d-127">Si nécessaire, vous serez invité à sélectionner un abonnement Azure à utiliser pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-127">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5fd3d-128">Certaines ressources Azure sont toujours utilisées pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-128">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="5fd3d-129">Exécutez `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-129">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> <span data-ttu-id="5fd3d-130">**Quelle est la différence entre approvisionnement et déploiement ?**</span><span class="sxs-lookup"><span data-stu-id="5fd3d-130">**What's the difference between Provision and Deploy?**</span></span>
>
> <span data-ttu-id="5fd3d-131">**L’étape** de mise en service crée des ressources dans Azure et M365 pour votre application, mais aucun code (HTML, CSS, JavaScript, etc.) n’est copié dans les ressources.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-131">The **Provision** step will create resources in Azure and M365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources.</span></span>  <span data-ttu-id="5fd3d-132">**L’étape** de déploiement copie le code de votre application vers les ressources que vous avez créées au cours de l’étape de mise en service.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-132">The **Deploy** step will copy the code for your app to the resources you created during the provision step.</span></span>  <span data-ttu-id="5fd3d-133">Il est courant de déployer plusieurs fois sans mettre en service de nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-133">It is common to deploy multiple times without provisioning new resources.</span></span> <span data-ttu-id="5fd3d-134">Étant donné que l’étape de mise en service peut prendre un certain temps, elle est distincte de l’étape de déploiement.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-134">Since the provision step can take some time to complete, it is separate from the deployment step.</span></span>

<span data-ttu-id="5fd3d-135">Une fois les étapes d’approvisionnement et de déploiement terminées :</span><span class="sxs-lookup"><span data-stu-id="5fd3d-135">Once the provisioning and deployment steps are finished:</span></span>

1. <span data-ttu-id="5fd3d-136">À Visual Studio Code, ouvrez le panneau de débogage (**Ctrl+Shift+D**  /  **⌘⇧-D** ou **Afficher > exécuter**)</span><span class="sxs-lookup"><span data-stu-id="5fd3d-136">From Visual Studio Code, open the debug panel (**Ctrl+Shift+D** / **⌘⇧-D** or **View > Run**)</span></span>
1. <span data-ttu-id="5fd3d-137">Sélectionnez **Lancer à distance (Edge)** dans la zone de configuration de lancement.</span><span class="sxs-lookup"><span data-stu-id="5fd3d-137">Select **Launch Remote (Edge)** from the launch configuration drop-down.</span></span>
1. <span data-ttu-id="5fd3d-138">Appuyez sur le bouton Lire pour lancer votre application, désormais en cours d’exécution à distance à partir d’Azure !</span><span class="sxs-lookup"><span data-stu-id="5fd3d-138">Press the Play button to launch your app - now running remotely from Azure!</span></span>
