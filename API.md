# API TerrangaFood — Documentation

## Base URL
```
http://localhost:3001/api
```

---

## Restaurants (existant)

| Méthode | Endpoint | Description |
|---------|----------|-------------|
| GET | /api/restaurants | Lister tous les restaurants |
| GET | /api/restaurants/:id | Détail d'un restaurant |
| POST | /api/restaurants | Créer un restaurant |
| PUT | /api/restaurants/:id | Modifier un restaurant |
| DELETE | /api/restaurants/:id | Supprimer un restaurant |

---

## Plats (existant)

| Méthode | Endpoint | Description |
|---------|----------|-------------|
| GET | /api/plats | Lister tous les plats |
| GET | /api/plats/:id | Détail d'un plat |
| GET | /api/plats/restaurant/:restoId | Plats d'un restaurant |
| POST | /api/plats | Créer un plat |
| PUT | /api/plats/:id | Modifier un plat |
| DELETE | /api/plats/:id | Supprimer un plat |

---

## Commandes (Lab 1 — NOUVEAU)

| Méthode | Endpoint | Description |
|---------|----------|-------------|
| POST | /api/commandes | Créer une commande |
| GET | /api/commandes | Lister toutes les commandes |
| GET | /api/commandes/:id | Détail d'une commande |
| PATCH | /api/commandes/:id/statut | Changer le statut |
| DELETE | /api/commandes/:id | Supprimer une commande |

---

### POST /api/commandes — Créer une commande

**Body JSON requis :**

```json
{
  "client": "Moussa Diop",
  "telephone": "+221 77 123 45 67",
  "adresseLivraison": "Cité Keur Gorgui, Villa 12, Dakar",
  "restaurant": "ID_RESTAURANT",
  "plats": ["ID_PLAT_1", "ID_PLAT_2"],
  "montantTotal": 4500,
  "commentaire": "Sans piment svp"
}
```

**Champs :**

| Champ | Type | Requis | Description |
|-------|------|--------|-------------|
| client | String | Oui | Nom du client (max 100 caractères) |
| telephone | String | Oui | Numéro de téléphone du client |
| adresseLivraison | String | Oui | Adresse de livraison à Dakar |
| restaurant | ObjectId | Oui | ID du restaurant |
| plats | [ObjectId] | Oui | Tableau d'IDs de plats commandés |
| montantTotal | Number | Oui | Montant total en FCFA (≥ 0) |
| commentaire | String | Non | Instruction spéciale (max 300 caractères) |

**Réponse 201 Created :**

```json
{
  "_id": "665b2c...",
  "client": "Moussa Diop",
  "telephone": "+221 77 123 45 67",
  "adresseLivraison": "Cité Keur Gorgui, Villa 12, Dakar",
  "restaurant": "664a1b...",
  "plats": ["664a2d...", "664a2e..."],
  "montantTotal": 4500,
  "statut": "en attente",
  "commentaire": "Sans piment svp",
  "createdAt": "2025-...",
  "updatedAt": "2025-..."
}
```

---

### GET /api/commandes — Lister les commandes

Retourne toutes les commandes triées par date de création (plus récentes en premier).
Les champs `restaurant` et `plats` sont automatiquement peuplés (populate).

**Réponse 200 OK :** tableau de commandes avec noms de restaurants et plats inclus.

---

### GET /api/commandes/:id — Détail d'une commande

**Réponse 200 OK :** commande complète avec :
- `restaurant` : `{ nom, adresse, telephone }`
- `plats` : `[{ nom, prix, categorie }]`

**Réponse 404 Not Found :**
```json
{ "message": "Commande non trouvée" }
```

---

### PATCH /api/commandes/:id/statut — Changer le statut

**Body JSON :**
```json
{ "statut": "confirmée" }
```

**Transitions autorisées :**

```
en attente  →  confirmée  →  en livraison  →  livrée
en attente  →  annulée
confirmée   →  annulée
```

**Réponse 200 OK :** commande mise à jour.

**Réponse 400 Bad Request (transition interdite) :**
```json
{
  "message": "Transition impossible",
  "details": "\"confirmée\" ne peut pas devenir \"livrée\"",
  "transitionsAutorisees": ["en livraison", "annulée"]
}
```

---

### DELETE /api/commandes/:id — Supprimer une commande

**Réponse 200 OK :**
```json
{ "message": "Commande supprimée avec succès" }
```

**Réponse 404 Not Found :**
```json
{ "message": "Commande non trouvée" }
```

---

## Codes HTTP

| Code | Signification |
|------|--------------|
| 200 | Succès |
| 201 | Ressource créée avec succès |
| 400 | Données invalides ou transition de statut interdite |
| 404 | Ressource non trouvée |
| 500 | Erreur interne du serveur |

---

## Notes techniques

- Les IDs (`restaurant`, `plats`) doivent être des ObjectId MongoDB valides.
- Le champ `statut` est automatiquement initialisé à `"en attente"` à la création.
- Les timestamps `createdAt` et `updatedAt` sont gérés automatiquement par Mongoose.
- Le populate remplace les ObjectId par les données réelles (équivalent d'un JOIN SQL).
