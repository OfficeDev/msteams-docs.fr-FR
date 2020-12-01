### <a name="_layoutcshtml"></a>_Layout. cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **Kit de développement logiciel (SDK) JavaScript client Microsoft teams** et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page. Voici comment votre onglet et le client teams communiquent :

- Naviguez jusqu’au dossier **partagé** , ouvrez **_Layout. cshtml** et ajoutez ce qui suit à la `<head>` balise :

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
>Ne copiez pas/collez les `<script src="...">` URL à partir de cette page, car elles ne représentent pas nécessairement la dernière version. Pour obtenir la dernière version du kit de développement logiciel (SDK), accédez toujours à : [Microsoft teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).

### <a name="tabcshtml"></a>Tab. cshtml

Ouvrez **Tab. cshtml** et mettez à jour l’incorporé `<script>` comme suit :

- En haut du script, appelez `microsoftTeams.initialize()` .

- Mettez à jour les `websiteUrl` `contentUrl` valeurs et dans chaque fonction avec l’URL HTTPS ngrok sur votre onglet.

Votre code doit maintenant ressembler à ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :

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

Veillez à enregistrer la **tabulation. cshtml** mise à jour.

## <a name="build-and-run-your-application"></a>Création et exécution de votre application

- Dans Visual Studio, appuyez sur **F5** ou sélectionnez **Démarrer le débogage** dans le menu **Déboguer** . Vérifiez que **ngrok** est en cours d’exécution et qu’il fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok qui a été fournie dans votre fenêtre d’invite de commandes.

>[!TIP]
>Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour qu’elle fonctionne, **laissez ngrok en cours d’exécution**. Il continuera à écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarrera dans Visual Studio. Si vous devez redémarrer le service ngrok, il renverra une nouvelle URL et vous devrez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-tab-to-teams-with-app-studio"></a>Télécharger votre onglet vers teams avec App Studio

>[!Note]
> Nous utilisons App Studio pour modifier votre **manifest.jssur** fichier et télécharger le package terminé vers Teams. Si vous le souhaitez, vous pouvez également modifier manuellement le **manifest.jssur** le fichier. Si vous le faites, veillez à créer à nouveau la solution pour créer le fichier **tab.zip** à télécharger.

- Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.

- Ouvrez l’application Studio et sélectionnez l’onglet **éditeur de manifeste** .

- Sélectionnez la vignette **Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est fourni avec son propre manifeste partiellement complet. Le nom de votre package d’application est **tab.zip**. Il doit se trouver ici :

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- Téléchargez **tab.zip** vers l’application Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez téléchargé votre package d’application dans App Studio, vous devez terminer de le configurer.

- Sélectionnez la mosaïque de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.

Il y a une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre *manifest.js* , mais il existe quelques champs que vous devrez mettre à jour :

#### <a name="details-app-details"></a>Détails : détails de l’application

- Sous *identification* sélectionnez ***générer** _ pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.

- Sous _Developer informations *, mettez à jour le champ **URL du site Web** avec votre URL HTTPS *ngrok* .

- Sous *URL* de l’application, mettez à jour les champs **déclaration de confidentialité** et **conditions d’utilisation** avec votre URL HTTPS *ngrok* . N’oubliez pas d’inclure les chemins d’accès */Privacy* et */tou* à la fin des URL.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section *onglets* :

- Sous l' *onglet équipe* , sélectionnez **Ajouter**.

- Dans la fenêtre contextuelle de l’onglet équipe, mettez à jour l' *URL de configuration* vers `https://<yourngrokurl>/tab` .

- Enfin, assurez-vous que la *mise à jour de la configuration est possible ?* Les cases Team et *Group chat* sont cochées, puis sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Terminer : domaines et autorisations

Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL ngrok sans le préfixe https- `<yourngrokurl>.ngrok.io/` .

#### <a name="test-and-distribute-test-and-distribute"></a>Test et distribution : test et distribution

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
