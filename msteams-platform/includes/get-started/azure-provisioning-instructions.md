## <a name="deploy-your-app-to-azure"></a>Déployer votre application sur Azure

Le déploiement se compose de deux étapes.  Tout d’abord, les ressources cloud nécessaires sont créées (également appelées approvisionnement), puis le code qui constitue votre application est copié dans les ressources cloud créées.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Sélectionnez le Teams Shared Computer Toolkit la barre latérale en sélectionnant l’icône Teams côté.
1. Sélectionnez **Provision dans le cloud**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement":::

1. Si nécessaire, sélectionnez un abonnement à utiliser pour les ressources Azure.

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

1. Une boîte de dialogue vous avertit que des coûts peuvent être encourus lors de l’exécution de ressources dans Azure.  Appuyez **sur Provision**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="Capture d’écran de la boîte de dialogue d’approvisionnement.":::

   Le processus de mise en service crée des ressources dans le cloud Azure. Cela prend un certain temps. Vous pouvez surveiller la progression en regardant les boîtes de dialogue dans le coin inférieur droit. Après quelques minutes, vous voyez l’avis suivant :

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée.":::

1. Une fois l’approvisionnement terminé, **sélectionnez Déployer dans le cloud.**  Comme pour l’approvisionnement, ce processus prend un certain temps.  Vous pouvez surveiller le processus en regardant les boîtes de dialogue dans le coin inférieur droit. Après quelques minutes, vous voyez un avis d’achèvement.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Dans la fenêtre de votre terminal :

1. Exécutez `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Vous pouvez être invité à vous connecter à votre abonnement Azure. Si nécessaire, vous êtes invité à sélectionner un abonnement Azure à utiliser pour les ressources Azure.

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

1. Exécutez `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> **Quelle est la différence entre approvisionnement et déploiement ?**
>
> **L’étape** de mise en service crée des ressources dans Azure et M365 pour votre application, mais aucun code (HTML, CSS, JavaScript, etc.) n’est copié dans les ressources. **L’étape** Déployer copie le code de votre application vers les ressources que vous avez créées au cours de l’étape de mise en service. Il est courant de déployer plusieurs fois sans mettre en service de nouvelles ressources. Étant donné que l’étape de mise en service peut prendre un certain temps, elle est distincte de l’étape de déploiement.

Une fois les étapes d’approvisionnement et de déploiement terminées :

1. À Visual Studio Code, ouvrez le panneau de débogage (**Ctrl+Shift+D**  /  **⌘⇧-D** ou **Afficher > exécuter**)
1. Sélectionnez **Lancer à distance (Edge)** dans la zone de configuration de lancement.
1. Appuyez sur le bouton Lire pour lancer votre application, désormais en cours d’exécution à distance à partir d’Azure !
