# Rapport de tests - Lab 3 (Docker)

## Équipe : les nazis
## Testeur : Idrissa Kane (QA)

### Images Docker
| # | Test | OK ? | Notes |
|---|--------------------------------------|------|-----------|
| 1 | docker build API réussit | ✅ | Build sans erreur |
| 2 | docker build Frontend réussit | ✅ | Build sans erreur |
| 3 | Image API < 250 Mo | ✅ | Conforme au seuil |
| 4 | Image Frontend < 500 Mo | ✅ | Conforme au seuil |

### Docker Compose
| # | Test | OK ? | Notes |
|---|--------------------------------------|------|-----------|
| 5 | docker compose up --build réussit | ✅ | 3 services démarrés |
| 6 | 3 conteneurs en état "Up" | ✅ | mongo, api, web |
| 7 | Seed fonctionne dans le conteneur | ✅ | 5 restos + 27 plats |
| 8 | API répond sur localhost:3001 | ✅ | Endpoints OK |
| 9 | Frontend répond sur localhost:3000 | ✅ | Interface OK |

### Fonctionnel
| # | Test | OK ? | Notes |
|---|--------------------------------------|------|-----------|
| 10| Restaurants affichés | ✅ | 5 restaurants visibles |
| 11| Commande créée via formulaire | ✅ | Message de succès |
| 12| Commande visible dans mes-cmds | ✅ | Badge + montant OK |
| 13| Données persistent après restart | ✅ | Volume fonctionne |
| 14| docker compose down fonctionne | ✅ | Conteneurs arrêtés |
| 15| docker compose down -v vide la DB | ✅ | Volume supprimé |

## Résumé
Tous les tests sont passés avec succès. L'application est entièrement conteneurisée 
et fonctionne de manière identique à l'environnement de développement local. 
Le volume Docker assure la persistance des données entre les redémarrages.