### <a name="_layoutcshtml"></a>_Layout.cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page. Voici comment votre onglet et le client Teams communiquent :

Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> Ne copiez pas et collez les URL de cette page, car elles peuvent ne pas représenter `<script src="...">` la dernière version. Pour obtenir la dernière version du SDK, toujours Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).

### <a name="tabcshtml"></a>Tab.cshtml

**Pour mettre à jour le script incorporé**

1. Dans Visual Studio, **ouvrez Tab.cshtml** pour mettre à jour l’incorporé `<script>` .

1. En haut du script, appelez `microsoftTeams.initialize()` .

1. Mettez à `websiteUrl` jour les `contentUrl` valeurs de chaque fonction avec l’URL HTTPS ngrok sur votre onglet.

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

1. Veillez à enregistrer le **tab.cshtml mis à jour.**

## <a name="build-and-run-your-application"></a>Créer et exécuter votre application

Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.** Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.

> [!TIP]
> Votre application doit être en cours d’exécution Visual Studio et ngrok. Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **ngrok est toujours en cours d’exécution.** Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio. Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-tab"></a>Télécharger onglet

>[!Note]
> App Studio peut être utilisé pour modifier votre **manifest.jsfichier** et télécharger le package terminé dans Teams. Vous pouvez également modifier manuellement le **fichiermanifest.jssi** vous préférez. Si vous le faites, assurez-vous de générer à nouveau la solution pour créertab.zip **fichier** à télécharger.

**Pour télécharger votre onglet**

1. Go to Microsoft Teams. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)

1. Go to **App Studio** and select the **Manifest editor** tab.

1. Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet. Le nom de votre package d’application **esttab.zip**. Il est disponible ici :

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Télécharger **tab.zip** app Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Mettre à jour votre package d’application avec l’éditeur de manifeste

Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.

Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.

Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes. La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs :

#### <a name="details-app-details"></a>Détails : détails de l’application

Dans la section **Détails de l’application** :

1. Sous **Identification,** **sélectionnez Générer** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.

1. Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**

1. Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Dans la section **Onglets** :

1. Sous **l’onglet Équipe,** **sélectionnez Ajouter.**

1. Dans la fenêtre **pop-up de** l’onglet Équipe, mettez à jour l’URL **de configuration** sur `https://<yourngrokurl>/tab` .

1. Assurez-vous **que les case**  à cocher Mettre à jour la configuration ? , **Équipe** et Groupe sont sélectionnées et sélectionnez **Enregistrer**.

#### <a name="finish-domains-and-permissions"></a>Finish: Domains and permissions

Dans la section **Domaines et autorisations,** les domaines de vos **onglets** doivent contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`

#### <a name="finish-test-and-distribute"></a>Fin : Tester et distribuer

>[!IMPORTANT]
> À droite, dans **Description,** vous voyez l’avertissement suivant :
>
> &#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »
>
> Cet avertissement peut être ignoré lors du test de votre onglet.

1. Dans la section **Tester et distribuer,** sélectionnez **Installer.**

1. Dans la boîte de dialogue  de fenêtre instantanée, sélectionnez Ajouter à une équipe ou, dans la zone de la boîte de dialogue, sélectionnez Ajouter **à une conversation.**

1. Choisissez l’équipe ou la conversation dans laquelle vous souhaitez afficher l’onglet, puis sélectionnez **Configurer un onglet.**

1. Dans la boîte de dialogue de fenêtre pop-up suivante, sélectionnez **Gris** ou **Rouge,** puis sélectionnez **Enregistrer.**

1. Pour afficher votre onglet, allez dans l’équipe où vous avez installé l’onglet, puis sélectionnez-le dans la barre d’onglets. La page que vous avez choisie lors de la configuration s’affiche.

    ![Onglet canal ASPNETMVC chargé](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

