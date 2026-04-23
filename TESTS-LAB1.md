# Rapport de tests -- Lab 1

## Équipe : [les nazis]
## Testeur : [Ibrahima gueye] (QA)

| # | Test | Résultat | Notes |
|---|----------------------------------|-----------|----------------------------------------------------|
| 1 | POST commande valide | OK | Commande créée avec statut "en attente" par défaut. |
| 2 | POST commande sans client | OK | Erreur 400 reçue avec messages de validation. |
| 3 | GET toutes les commandes | OK | Liste de toutes les commandes récupérée avec succès. |
| 4 | GET commande par ID | OK | Détails de la commande spécifique affichés. |
| 5 | GET commande ID inexistant | OK | Retourne une erreur 404 comme prévu. |
| 6 | PATCH en attente → confirmée | OK | Transition autorisée effectuée avec succès. |
| 7 | PATCH confirmée → en livraison | OK | Transition autorisée effectuée avec succès. |
| 8 | PATCH en livraison → livrée | OK | Transition finale effectuée avec succès. |
| 9 | PATCH transition interdite | OK | Erreur 400 : passage direct "confirmée" vers "livrée" bloqué. |
| 10| PATCH commande livrée | OK | Blocage de toute modification sur une commande terminée. |
| 11| DELETE commande | OK | Suppression fonctionnelle dans la base de données. |
| 12| Populate restaurant visible | OK | Le nom et l'adresse du restaurant sont bien affichés. |
| 13| Populate plats visible | OK | Les détails des plats sont bien inclus dans la réponse. |