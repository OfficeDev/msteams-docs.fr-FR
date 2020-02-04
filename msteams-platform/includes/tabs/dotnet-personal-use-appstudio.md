## <a name="upload-your-tab-to-teams-with-app-studio"></a>Télécharger votre onglet vers teams avec App Studio

>[!NOTE]
> Nous utilisons App Studio pour modifier votre fichier **Manifest. JSON** et télécharger le package terminé vers Teams. Vous pouvez également modifier manuellement le **fichier manifest. JSON** si vous le souhaitez. Si vous le faites, veillez à créer à nouveau la solution pour créer le fichier **. zip de tabulation** à télécharger.

- Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.

- Ouvrez l’application Studio et sélectionnez l’onglet **éditeur de manifeste** .

- Sélectionnez la vignette **Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est fourni avec son propre manifeste partiellement complet. Le nom de votre package d’application est **Tab. zip**. Il doit se trouver ici :

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- Téléchargez **Tab. zip** dans App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez téléchargé votre package d’application dans App Studio, vous devez terminer de le configurer.

- Sélectionnez la mosaïque de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.

Il y a une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre *fichier manifest. JSON* , mais il existe quelques champs que vous devrez mettre à jour :

#### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section Détails de l' *application* :

- Sous *identification* , sélectionnez **générer** pour générer un nouvel ID d’application pour votre application.

- Sous *informations sur le développeur* , mettez à jour l' **URL du site Web** avec votre URL HTTPS *ngrok* .

- Sous *URL* de l’application **** `https://<yourngrokurl>/privacy` , mettez à jour la déclaration de confidentialité et les **conditions d’utilisation** pour `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section *onglets* :

- Sous *Ajouter un onglet personnel* , sélectionnez ***Ajouter***. Une fenêtre de boîte de dialogue contextuelle s’affiche.

- Renseignez le champ *nom* .

- Renseignez le champ ID de l' *entité* .

- Mettez à jour le champ *URL* du `https://<yourngrokurl>/personalTab`contenu avec la valeur à.

- Laissez le champ *URL du site Web* vide.

- Cliquez sur ***Enregistrer***.

#### <a name="finish-domains-and-permissions"></a>Terminer : domaines et autorisations

Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io/`HTTPS-.

##### <a name="finish-test-and-distribute"></a>Terminer : tester et distribuer

>[!IMPORTANT]
>Dans le champ **Description** à droite, vous verrez l’avertissement suivant :
>
>&#9888;**le tableau « validDomains » ne peut pas contenir de site de tunneling...**
>
>Cet avertissement peut être ignoré lors du test de votre onglet.

Dans la section *test et distribution* :

- Sélectionnez **Installer**.

- Dans la fenêtre contextuelle, assurez-vous que l’option *Ajouter pour vous* est définie sur *Oui* et *Ajouter à une équipe ou une conversation* est définie sur *non*.

- Sélectionnez **Installer**.

- Dans la fenêtre contextuelle suivante, sélectionnez **ouvrir** et votre onglet est affiché.

## <a name="view-your-personal-tab"></a>Affichage de votre onglet personnel

- Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez `...` le menu. Une liste d’applications personnelles s’affiche.

- Sélectionnez votre onglet dans la liste à afficher.
