## <a name="upload-your-tab-to-teams-with-app-studio"></a>Télécharger votre onglet pour Teams avec App Studio

>[!NOTE]
> Nous utilisons App Studio pour modifier vos **manifest.jsdans le** fichier et télécharger le paquet terminé à Teams. Vous pouvez également modifier manuellement **manifest.jssur si** vous préférez. Si vous le faites, assurez-vous de construire la solution à nouveau pour **créerTab.zip** fichier à télécharger.

- Ouvrez le Microsoft Teams client. Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).

- Ouvrez le studio App et sélectionnez **l’onglet Éditeur** Manifeste.

- Sélectionnez **l’importation d’une vignette d’application** existante dans l’éditeur Manifeste pour commencer à mettre à jour le paquet d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il devrait être trouvé ici:

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- Télécharger **Tab.zipà** App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettez à jour votre package d’application avec l’éditeur Manifest

Une fois que vous avez téléchargé votre paquet d’applications dans App Studio, vous devrez finir de le configurer.

- Sélectionnez la vignette pour votre onglet nouvellement importé dans le panneau droit de la page de bienvenue de l’éditeur Manifeste.

Il ya une liste d’étapes dans le côté gauche de l’éditeur Manifeste, et sur la droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. Une grande partie de l’information a été *fournie parmanifest.jssur,* mais il ya quelques domaines que vous aurez besoin de mettre à jour:

#### <a name="details-app-details"></a>Détails: Détails de l’application

Dans la section **Détails de l’application** :

- Sous **Identification** **sélectionnez Générer** pour générer un nouvel id d’application pour votre application.

- Sous les **informations du développeur** mettre à jour **l’URL** du site Web avec votre URL **HTTPS ngrok.**

- Sous **les URL d’application mettre à** jour **l’instruction de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Capacités: Onglets

Dans la section *Onglets* :

- Sous **Ajouter un onglet personnel sélectionnez** **Ajouter**. Vous serez présenté avec une fenêtre de dialogue pop-up.

- Complétez le **champ** Nom.

- Complétez le champ **Id entité.**

- Mettez à jour **le champ URL** de contenu avec à `https://<yourngrokurl>/personalTab` .

- Laissez le champ **URL du** site Web vide.

- Sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Finition : Domaines et autorisations

Dans la section **Domaines et autorisations,** les **domaines de votre champ onglets** doivent contenir votre URL ngrok sans préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .

##### <a name="finish-test-and-distribute"></a>Finition: Test et distribuer

>[!IMPORTANT]
>Dans le **champ Description** à droite, vous verrez l’avertissement suivant :
>
>&#9888; "**Le tableau « validDomains » ne peut pas contenir un site de tunnelage...**»
>
>Cet avertissement peut être ignoré lors de l’essai de votre onglet.

Dans la section **Test et distribution** :

- Sélectionnez **Installer**.

- Dans la fenêtre pop-up assurez-vous que **Ajouter pour vous** est défini sur **Oui** et Ajouter à une équipe **ou chat** est défini à **No**.

- Sélectionnez **Installer**.

- Dans la prochaine fenêtre **contexturée, sélectionnez Ouvrir** et votre onglet s’affiche.

## <a name="view-your-personal-tab"></a>Consultez votre onglet personnel

- Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez le `...` menu. Vous serez présenté avec une liste d’applications personnelles.

- Sélectionnez votre onglet dans la liste à afficher.
