## <a name="upload-your-tab-with-app-studio"></a>Télécharger onglet avec App Studio

>[!NOTE]
> Nous utilisons **App Studio** pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams. Vous pouvez également modifier manuellement **manifest.jssur**. Si vous le faites, veillez à générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.

**Pour télécharger votre onglet avec App Studio**

1. Go to Microsoft Teams. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)

1. Go to **App Studio** and select the **Manifest editor** tab.

1. Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet.  Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il est disponible à partir du chemin d’accès suivant :

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Télécharger **tab.zip** **app Studio.**

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Après avoir chargé votre package d’application dans App Studio, vous devez le configurer.

Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.

Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs.

#### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section **Détails de l’application** :

1. Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.

1. Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**

1. Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section **Onglets** :

1. Sous **Ajouter un onglet personnel,** sélectionnez **Ajouter.** Une boîte de dialogue s’affiche.

1. Entrez un nom pour l’onglet personnel dans **Nom**.

1. Entrez **l’ID d’entité**.

1. Mettre à **jour l’URL de** contenu avec `https://<yourngrokurl>/personalTab` .

    Laissez le **champ URL** du site web vide.

1. Sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Finish: Domains and permissions

Dans la section **Domaines et autorisations,** le champ Domaines de vos **onglets** doit contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`

##### <a name="finish-test-and-distribute"></a>Fin : Tester et distribuer

>[!IMPORTANT]
> À droite, dans **Description,** vous voyez l’avertissement suivant :
>
> &#9888; tableau **« validDomains » ne peut pas contenir de site de tunneling...**
>
>Cet avertissement peut être ignoré lors du test de votre onglet.

1. Dans la section **Tester et distribuer,** sélectionnez **Installer.**

1. Dans la boîte de dialogue qui s’affiche, **sélectionnez** Ajouter et votre onglet s’affiche avec deux options.

1. Dans les options de l’onglet, **sélectionnez Gris** ou **Rouge.** L’onglet s’affiche en fonction de la couleur que vous avez sélectionnée.
 
    ![Onglet personnel ASPNETMVC chargé](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a>Afficher votre onglet personnel

1. Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF;. Une liste d’applications personnelles s’affiche.

1. Sélectionnez votre onglet dans la liste pour l’afficher.
