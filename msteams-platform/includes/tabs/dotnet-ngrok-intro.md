## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft Teams est un produit basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local. Vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui expose votre port local à une URL internet.

Pour tester votre onglet, utilisez [ngrok](https://ngrok.com/docs). Les points de terminaison web de votre serveur sont disponibles lorsque ngrok est en cours d’exécution sur votre ordinateur. Dans la version gratuite de ngrok, si vous fermez ngrok, les URL sont différentes lors du prochain démarrage.