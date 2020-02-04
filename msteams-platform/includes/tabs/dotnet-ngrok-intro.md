## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft teams est un produit entièrement basé sur le Cloud et nécessite que le contenu de votre onglet soit disponible dans le nuage à l’aide de points de terminaison HTTPs. Teams n’autorise pas l’hébergement local. Vous devrez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL accessible sur Internet.

Pour tester votre onglet, vous utiliserez [ngrok](https://ngrok.com/docs). Les points de terminaison Web de votre serveur seront disponibles pendant l’exécution d’ngrok sur votre ordinateur local. Si vous fermez ngrok, les URL seront différentes lors du prochain démarrage.