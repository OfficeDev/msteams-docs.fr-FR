## <a name="deploy-your-app-to-azure"></a>Déployer votre application sur Azure

Le déploiement se compose de deux étapes.  Tout d’abord, les ressources cloud nécessaires sont créées (également appelées approvisionnement). Ensuite, le code de votre application est copié dans les ressources cloud créées. Pour ce didacticiel, vous allez déployer l’application Onglet.

> <details>
> <summary>Quelle est la différence entre approvisionnement et déploiement ?</summary>
>
> **L’étape** de mise en service crée des ressources dans Azure et Microsoft 365 pour votre application, mais aucun code (HTML, CSS, JavaScript, etc.) n’est copié dans les ressources. **L’étape** Déployer copie le code de votre application vers les ressources que vous avez créées au cours de l’étape de mise en service. Il est courant de déployer plusieurs fois sans mettre en service de nouvelles ressources. Étant donné que l’étape de mise en service peut prendre un certain temps, elle est distincte de l’étape de déploiement.
</details>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Sélectionnez l’icône :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: du kit de ressources Teams dans la barre latérale Visual Studio Code.

1. **Sélectionnez Provision dans le cloud**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement" border="false":::

1. Sélectionnez un abonnement à utiliser pour les ressources Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Capture d’écran montrant les ressources pour l’approvisionnement" border="false":::

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

    Une boîte de dialogue vous avertit que des coûts peuvent être encourus lors de l’exécution de ressources dans Azure.

1. Sélectionnez **Provision**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Capture d’écran de la boîte de dialogue d’approvisionnement." border="false":::

   Le processus de mise en service crée des ressources dans le cloud Azure. Cela peut prendre un certain temps. Vous pouvez surveiller la progression en regardant les boîtes de dialogue dans le coin inférieur droit. Après quelques minutes, vous voyez l’avis suivant :

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-success.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée." border="false":::

    Si vous le souhaitez, vous pouvez afficher les ressources provisionées. Pour ce didacticiel, vous n’avez pas besoin d’afficher les ressources.

    La ressource mise en service apparaît dans la section **Environnement** .

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Capture d’écran montrant la boîte de dialogue de mise en service terminée." border="false":::

1. **Sélectionnez Déployer dans le cloud à** partir du panneau **Déploiement** une fois l’approvisionnement terminé.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Capture d’écran montrant l’endroit où cliquer pour déployer dans le cloud." border="false":::

   Comme pour l’approvisionnement, le déploiement prend un certain temps. Vous pouvez surveiller le processus en regardant les boîtes de dialogue dans le coin inférieur droit. Après quelques minutes, vous voyez un avis d’achèvement.

À présent, vous pouvez utiliser le même processus pour déployer vos applications bot et d’extension de message dans Azure.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Dans la fenêtre de votre terminal :

1. Exécutez `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Lorsque vous y est invité, sélectionnez un abonnement Azure pour utiliser les ressources Azure.

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

1. Exécutez `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Exécuter l’application déployée

Une fois les étapes d’approvisionnement et de déploiement terminées :

1. Ouvrez le panneau de débogage (**Ctrl+Shift+D** / **⌘⇧-D** ou **Afficher > exécuter**) à partir Visual Studio Code.
1. **Sélectionnez Lancer à distance (Edge)** dans la zone de configuration de lancement.
1. Sélectionnez le bouton Lire pour lancer votre application à partir d’Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Capture d’écran montrant l’application de lancement à distance." border="false":::

1. Sélectionnez **Ajouter**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Capture d’écran montrant l’application en cours d’installation." border="false":::

   Votre application est chargée sur le site Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-app.png" alt-text="Capture d’écran montrant l’application en cours d’installation." border="false":::

    Félicitations ! Votre application onglet s’exécute désormais à distance à partir d’Azure !
