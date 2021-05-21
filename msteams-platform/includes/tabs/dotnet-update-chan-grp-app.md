### <a name="_layoutcshtml"></a>_Layout.cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page. Voici comment votre onglet et le client Teams communiquent :

- Accédez au **dossier** partagé, **ouvrez _Layout.cshtml** et ajoutez ce qui suit à la `<head>` balise :

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
>Ne copiez/collez pas les URL de cette page, car elles peuvent ne pas représenter `<script src="...">` la dernière version. Pour obtenir la dernière version du SDK, toujours aller à : [Microsoft Teams API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).

### <a name="tabcshtml"></a>Tab.cshtml

Ouvrez **Tab.cshtml** et mettez à jour l’incorporé `<script>` comme suit :

- En haut du script, appelez `microsoftTeams.initialize()` .

- Mettez à `websiteUrl` jour les `contentUrl` valeurs de chaque fonction avec l’URL HTTPS ngrok sur votre onglet.

Votre code doit maintenant ressembler à ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :

```javascript
    microsoftTeams.initialize();

    let saveGray = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                entityId: "grayIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }

    let saveRed = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                entityId: "redIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }
```

Veillez à enregistrer le **tab.cshtml mis à jour.**

## <a name="build-and-run-your-application"></a>Créer et exécuter votre application

- Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.** Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

>[!TIP]
>Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **ngrok est toujours en cours d’exécution.** Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio. Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-tab-to-teams"></a>Télécharger votre onglet pour Teams

>[!Note]
> Nous utilisons App Studio pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams. Vous pouvez également modifier manuellement le **fichiermanifest.jssi** vous préférez. Si vous le faites, assurez-vous de générer à nouveau la solution pour créertab.zip **fichier** à télécharger.

- Ouvrez le client Microsoft Teams client. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils [de développement de votre navigateur.](~/tabs/how-to/developer-tools.md)

- Ouvrez App studio et sélectionnez **l’onglet Éditeur de** manifeste.

- Sélectionnez **la vignette Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il doit être trouvé ici :

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- Télécharger **tab.zip** app Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.

- Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.

Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre *manifest.js,* mais il existe quelques champs que vous devrez mettre à jour :

#### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section *Détails de l’application* :

- *Identification*: **sélectionnez Générer** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.

- *Informations sur le* développeur : mettez à jour **le champ URL** du site web avec votre URL HTTPS *ngrok.*

- *URL d’application*: mettez à jour la déclaration **de confidentialité** et les `https://<yourngrokurl>/privacy` conditions **d’utilisation** `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section *Onglets* :

- *Onglet Équipe*: sélectionnez **Ajouter.**

- Dans la fenêtre pop-up de l’onglet Équipe, mettez à jour *l’URL de configuration* sur `https://<yourngrokurl>/tab` .

- Enfin, assurez-vous que la *configuration peut être mise à jour ? Les cases* de *conversation* d’équipe et de groupe sont cochées, puis **sélectionnez Enregistrer.**

#### <a name="finish-domains-and-permissions"></a>Finish: Domains and permissions

Dans la section *Domaines et autorisations* :

- Les *domaines du champ onglets* doivent contenir votre URL ngrok sans le préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .

#### <a name="finish-test-and-distribute"></a>Fin : Tester et distribuer

>[!IMPORTANT]
>Dans le **champ Description** à droite, vous verrez l’avertissement suivant :
>
>&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »
>
>Cet avertissement peut être ignoré lors du test de votre onglet.

Dans la section *Tester et distribuer* :

- Sélectionnez **Installer**.

- Dans le champ Ajouter à une équipe ou une *conversation* de la fenêtre pop-up, entrez votre équipe et sélectionnez **Installer.**

- Dans la fenêtre pop-up suivante, choisissez le canal d’équipe où vous souhaitez que l’onglet s’affiche, puis **sélectionnez Configurer.**

- Dans la fenêtre pop-up finale, sélectionnez une valeur pour la page d’onglet (icône rouge ou grise), puis sélectionnez **Enregistrer**.

Pour afficher votre onglet, accédez à l’équipe sur qui vous l’avez installé et sélectionnez-le dans la barre d’onglets. La page que vous avez choisie lors de la configuration doit être affichée.
