## <a name="upload-your-tab-to-teams-with-app-studio"></a>Télécharger votre onglet pour Teams avec App Studio

>[!NOTE]
> Nous utilisons App Studio pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams. Vous pouvez également modifier manuellement **manifest.jssi** vous préférez. Si vous le faites, n’oubliez pas de générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.

- Ouvrez le client Microsoft Teams client. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)

- Ouvrez App studio et sélectionnez **l’onglet Éditeur de** manifeste.

- Sélectionnez **la vignette Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il doit être trouvé ici :

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- Télécharger **Tab.zip** app Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.

- Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.

Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre *manifest.js,* mais il existe quelques champs que vous devrez mettre à jour :

#### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section **Détails de l’application** :

- Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.

- Sous **Informations du développeur,** mettez à jour **l’URL du site** web avec votre URL HTTPS **ngrok.**

- Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section *Onglets* :

- Sous **Ajouter un onglet personnel, sélectionnez** **Ajouter.** Une fenêtre de dialogue s’ouvrira.

- Remplissez le **champ** Nom.

- Terminez **le champ ID de l’entité.**

- Mettez à jour **le champ URL** de contenu avec `https://<yourngrokurl>/personalTab` .

- Laissez le **champ URL** du site web vide.

- Sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Finish: Domains and permissions

Dans la section **Domaines et autorisations,** le champ Domaines de vos **onglets** doit contenir votre URL ngrok sans le préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .

##### <a name="finish-test-and-distribute"></a>Fin : Tester et distribuer

>[!IMPORTANT]
>Dans le **champ Description** à droite, vous verrez l’avertissement suivant :
>
>&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »
>
>Cet avertissement peut être ignoré lors du test de votre onglet.

Dans la section **Tester et distribuer** :

- Sélectionnez **Installer**.

- Dans la fenêtre pop-up, assurez-vous que La valeur Ajouter pour vous est définie sur **Oui** et que l’ajout à une équipe ou à une **conversation** est définie sur **Non**. 

- Sélectionnez **Installer**.

- Dans la fenêtre pop-up suivante, sélectionnez **Ouvrir** et votre onglet s’affiche.

## <a name="view-your-personal-tab"></a>Afficher votre onglet personnel

- Dans la barre de navigation située à l’extrême gauche de l’Teams App, sélectionnez le `...` menu. Une liste d’applications personnelles vous sera présentée.

- Sélectionnez votre onglet dans la liste à afficher.
