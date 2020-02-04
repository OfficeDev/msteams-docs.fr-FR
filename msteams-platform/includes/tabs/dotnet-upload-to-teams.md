## <a name="upload-your-tab-to-teams-with-app-studio"></a>Télécharger votre onglet vers teams avec App Studio

>[!NOTE]
> Nous utilisons App Studio pour modifier votre fichier **Manifest. JSON** et télécharger le package terminé vers Teams. Vous pouvez également modifier manuellement le fichier **Manifest. JSON** si vous le souhaitez. Si vous le faites, veillez à créer à nouveau la solution pour créer le fichier **. zip de tabulation** à télécharger.

- Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.

- Ouvrez l’application App Studio et sélectionnez l’onglet **éditeur de manifeste** .

- Sélectionnez la vignette **Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est fourni avec son propre manifeste partiellement complet. Le nom de votre package d’application est **Tab. zip**. Il doit se trouver ici :

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- Téléchargez **Tab. zip** dans App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez téléchargé votre package d’application dans App Studio, vous devez terminer de le configurer.

- Sélectionnez la mosaïque de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.

Il y a une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre *fichier manifest. JSON* , mais il existe quelques champs que vous devrez mettre à jour :

#### <a name="details-app-details"></a>Détails : détails de l’application

- Sous *identification* , sélectionnez **générer** pour générer un nouvel ID d’application pour votre application.

- Sous *informations sur le développeur* , mettez à jour le champ **URL du site Web** avec votre URL HTTPS *ngrok* .

- Sous *URL* de l’application **** `https://<yourngrokurl>/privacy` , mettez à jour la déclaration de confidentialité et les **conditions d’utilisation** pour `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section *onglets* :

- Sous l' *onglet équipe* , sélectionnez **Ajouter**.

- Dans la fenêtre contextuelle de l’onglet équipe, mettez à jour l' `https://<yourngrokurl>/tab`URL de *configuration* vers.

- Enfin, assurez-vous que la *mise à jour de la configuration est possible ? *Les cases Team et *Group chat* sont cochées, puis sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Terminer : domaines et autorisations

Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io/`HTTPS-.

#### <a name="finish-test-and-distribute"></a>Terminer : tester et distribuer

>[!IMPORTANT]
>Dans le champ **Description** à droite, vous verrez l’avertissement suivant :
>
>&#9888;**le tableau « validDomains » ne peut pas contenir de site de tunneling...**
>
>Cet avertissement peut être ignoré lors du test de votre onglet.

Dans la section *test et distribution* :

- Sélectionnez **Installer**.

- Dans la fenêtre contextuelle *Ajouter à un champ d’équipe ou de conversation* , entrez votre équipe et sélectionnez **installer**.

- Dans la fenêtre contextuelle suivante, sélectionnez le canal d’équipe dans lequel vous souhaitez afficher l’onglet, puis sélectionnez **configurer**.

- Dans la fenêtre contextuelle finale, sélectionnez une valeur pour la page d’onglet (icône rouge ou gris) et sélectionnez **Enregistrer**.

Pour afficher votre onglet, accédez à l’équipe sur laquelle vous l’avez installé, puis sélectionnez-le dans la barre d’onglets. La page que vous avez choisie lors de la configuration doit s’afficher.
