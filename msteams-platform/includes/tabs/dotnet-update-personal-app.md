## <a name="update-your-application"></a>Mettre à jour votre application

### <a name="_layoutcshtml"></a>_Layout.cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page. Voici comment votre onglet et l’application Teams communiquent :

Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Ouvrez **PersonalTab.cshtml** et mettez à jour les `<script>` balises incorporées en appelant `microsoftTeams.initialize()` .

Veillez à enregistrer votre **fichier PersonalTab.cshtml** mis à jour.