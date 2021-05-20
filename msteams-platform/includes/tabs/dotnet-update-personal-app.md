## <a name="update-your-application"></a>Mettre à jour votre application

### <a name="_layoutcshtml"></a>_Layout.cshtml

Pour que votre onglet s’affiche Teams, vous devez **inclure le client javascript Microsoft Teams SDK** et inclure un appel `microsoftTeams.initialize()` après que votre page se charge. Voici comment votre onglet et l’application Teams communiquer :

- Accédez **au** dossier partagé, **ouvrez _Layout.cshtml** et ajoutez ce qui suit à la `<head>` section balises :

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Ouvrez **PersonalTab.cshtml et mettez** à jour les `<script>` balises intégrées en appelant `microsoftTeams.initialize()` .

Assurez-vous d’enregistrer votre **mise à jour PersonalTab.cshtml**.