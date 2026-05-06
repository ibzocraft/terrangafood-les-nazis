# Rapport de tests -- Lab 4 ( Production )

## Équipe : les nazis
## Testeur : Samba Laobe Seck ( QA )

## URLs de production
- Frontend : https://terrangafood-les-nazis.vercel.app
- API : https://terrangafood-api-les-nazis.onrender.com
- Atlas : mongodb+srv://terrangafood-admin:qnRJwB4b1yOsNu9G@terrangafood-lesnazis.b11vcc1.mongodb.net/terrangafood?appName=terrangafood-lesnazis

## Résultats
Résultats
|N°|	|Test                             |     |OK|
|1 |	|Page accueil affiche restaurants |	    |✅| 
|2 |	|Détail restaurant fonctionne     |	    |✅| 
|3 |	|Bouton commander ouvre formulaire|	    |✅|
|4 |	|Plats + prix affichés            |	    |✅|
|5 |	|Total dynamique fonctionne       |	    |✅|
|6 |	|Commande envoyée succès          |	    |✅| 
|7 |	|Commande visible                 |	    |✅| 
|8 |	|Statut correct (couleur)         |	    |✅| 
|9 |	|Infos correctes                  |	    |✅| 
|10|	|API restaurants                  |     |✅| 
|11|	|API commandes                    |	    |✅| 
|12|	|Données Atlas                    |     |✅| 


## Notes
- Temps de cold start API Render : ~XX secondes
- Bugs trouvés : aucun
- Test 12 : vérifié indirectement via l'API (GET /restaurants = 5 docs,
  GET /commandes = commandes visibles). Accès Atlas restreint au compte du DB.