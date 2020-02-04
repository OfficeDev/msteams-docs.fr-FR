## <a name="update-your-application"></a>Mettre à jour votre application

### <a name="_layoutcshtml"></a>_Layout. cshtml

Pour que votre onglet s’affiche dans Teams, vous devez inclure le **Kit de développement logiciel (SDK) JavaScript client Microsoft teams** et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page. Voici comment votre onglet et l’application teams communiquent :

- Naviguez jusqu’au dossier **partagé** , ouvrez **_Layout. cshtml**et ajoutez ce qui suit à `<head>` la section des balises :

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>PersonalTab. cshtml

Ouvrez **PersonalTab. cshtml** et mettez à jour `<script>` les balises `microsoftTeams.initialize()`incorporées en appelant.

Veillez à enregistrer votre mise à jour de *PersonalTab. cshtml*.