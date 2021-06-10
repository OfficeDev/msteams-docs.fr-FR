## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft Teams est un produit entièrement basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local. Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL internet.

Pour tester votre onglet, vous allez utiliser [ngrok.](https://ngrok.com/docs) Les points de terminaison web de votre serveur seront disponibles pendant l’exécution de ngrok sur votre ordinateur local. Si vous fermez ngrok, les URL seront différentes lors du prochain démarrage.