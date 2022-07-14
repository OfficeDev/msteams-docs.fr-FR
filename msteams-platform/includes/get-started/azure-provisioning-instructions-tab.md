## <a name="deploy-your-app-to-azure"></a>Déployer votre application vers Azure

Le déploiement se compose de deux étapes.  Tout d’abord, les ressources cloud nécessaires sont créées (également appelées approvisionnement). Ensuite, le code de votre application est copié dans les ressources cloud créées. Pour ce didacticiel, vous allez déployer l’application onglet.
<br>
<br>
<details>
<summary>Quelle est la différence entre provisionnement et déploiement ?</summary>
<br>
L’étape <b>De provisionnement</b> crée des ressources dans Azure et Microsoft 365 pour votre application, mais aucun code (HTML, CSS, JavaScript, etc.) n’est copié dans les ressources. L’étape <b>Déployer</b> copie le code de votre application dans les ressources que vous avez créées pendant l’étape de provisionnement. Il est courant de déployer plusieurs fois sans provisionner de nouvelles ressources. Étant donné que l’étape de provisionnement peut prendre un certain temps, elle est distincte de l’étape de déploiement.
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Sélectionnez l’icône :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: du kit de ressources Teams dans la barre latérale Visual Studio Code.

1. Sélectionnez **Provisionner dans le cloud**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Capture d’écran montrant les commandes d’approvisionnement":::

1. Sélectionnez un abonnement à utiliser pour les ressources Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Capture d’écran montrant les ressources pour l’approvisionnement":::

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

    Une boîte de dialogue vous avertit que des coûts peuvent être engagés lors de l’exécution de ressources dans Azure.

1. Sélectionnez **Provision**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Capture d’écran de la boîte de dialogue d’approvisionnement.":::

   Le processus d’approvisionnement crée des ressources dans le cloud Azure. Cela peut prendre un certain temps. Vous pouvez surveiller la progression en regardant les dialogues dans le coin inférieur droit. Après quelques minutes, vous voyez l’avis suivant :

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="Capture d’écran montrant la boîte de dialogue d’approvisionnement complet.":::

    Si vous le souhaitez, vous pouvez afficher les ressources approvisionnées. Pour ce didacticiel, vous n’avez pas besoin d’afficher les ressources.

    La ressource approvisionnée apparaît dans la section **Environnement** .

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Capture d’écran montrant la boîte de dialogue d’approvisionnement complet.":::

1. Sélectionnez **Déployer dans le cloud dans** le panneau **Déploiement** une fois l’approvisionnement terminé.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Capture d’écran montrant où cliquer pour déployer dans le cloud.":::

   Comme pour le provisionnement, le déploiement prend un certain temps. Vous pouvez surveiller le processus en regardant les dialogues dans le coin inférieur droit. Après quelques minutes, un avis d’achèvement s’affiche.

À présent, vous pouvez utiliser le même processus pour déployer vos applications Bot et Message Extension sur Azure.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Dans la fenêtre de votre terminal :

1. Exécutez `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Lorsque vous y êtes invité, sélectionnez un abonnement Azure pour utiliser des ressources Azure.

   > [!NOTE]
   > Certaines ressources Azure sont toujours utilisées pour héberger votre application.

1. Exécutez `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Exécuter l’application déployée

Une fois les étapes d’approvisionnement et de déploiement terminées :

1. Ouvrez le panneau de débogage (**Ctrl+Maj+D** / **⌘⇧-D** ou **Afficher > Exécuter**) à partir de Visual Studio Code.
1. Sélectionnez **Lancer à distance (Edge)** dans la liste déroulante de configuration de lancement.
1. Sélectionnez le bouton **Démarrer le débogage (F5)** pour lancer votre application à partir d’Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Capture d’écran montrant l’application de lancement à distance.":::

1. Sélectionnez **Ajouter** lorsque vous êtes invité à charger l’application sur Teams.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Capture d’écran montrant l’application en cours d’installation.":::

    Félicitations, votre première application onglet s’exécute dans votre environnement Azure !

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="Capture d’écran montrant le message permettant d’essayer l’application maintenant ou ultérieurement":::
 