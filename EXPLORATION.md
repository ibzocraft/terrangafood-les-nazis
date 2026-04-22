# Rapport d'exploration - Lab 0

## Équipe : Les Nazis

### Architecture Backend (par DB - [FAYE Cheikhou Oumar])
(À compléter par DB)

### Architecture Frontend (par DF - Idrissa Kane)
**Pages existantes :**

Le frontend utilise Next.js 14 avec l'App Router (nouveau système de routing).

1. **Page d'accueil** (`app/page.js`)
   - URL : `/`
   - Rôle : Affiche la liste complète des restaurants disponibles
   - Composant utilisé : RestaurantCard pour chaque restaurant

2. **Page de détail restaurant** (`app/restaurants/[id]/page.js`)
   - URL : `/restaurants/[id]` (route dynamique)
   - Rôle : Affiche les informations détaillées d'un restaurant et la liste de ses plats
   - Le `[id]` dans le nom du dossier indique une route dynamique Next.js
   - Composant utilisé : PlatCard pour chaque plat

3. **Layout global** (`app/layout.js`)
   - Rôle : Structure HTML de base commune à toutes les pages
   - Contient le composant Header qui s'affiche sur toutes les pages
   - Utilise le système de `children` pour injecter le contenu de chaque page

**Composants réutilisables :**

J'ai identifié 3 composants dans le dossier `components/` :

1. **Header.js**
   - Rôle : Barre de navigation avec le logo et le menu
   - Utilisé dans : `layout.js` (donc visible sur toutes les pages)
   - Contenu : Titre "TerrangaFood" et lien vers l'accueil

2. **RestaurantCard.js**
   - Rôle : Carte d'affichage d'un restaurant
   - Utilisé dans : `page.js` (page d'accueil)
   - Affiche : nom, type de cuisine, adresse, note
   - Reçoit les données via la prop `restaurant`

3. **PlatCard.js**
   - Rôle : Carte d'affichage d'un plat
   - Utilisé dans : `restaurants/[id]/page.js` (page de détail)
   - Affiche : nom du plat, description, prix
   - Reçoit les données via la prop `plat`

**Méthode d'appel API :**

Le frontend communique avec le backend via un fichier centralisé : `lib/api.js`

- **Méthode utilisée :** `fetch()` (fonction JavaScript native)
- **URL de base :** `http://localhost:3001/api`
- **Fonctions disponibles :**
  - `getRestaurants()` : Récupère la liste de tous les restaurants
    - Endpoint : GET /api/restaurants
  - `getRestaurantById(id)` : Récupère un restaurant spécifique
    - Endpoint : GET /api/restaurants/:id
  - `getPlats(restaurantId)` : Récupère les plats d'un restaurant
    - Endpoint : GET /api/restaurants/:id/plats

- **Utilisation :** Les pages importent ces fonctions via `import { ... } from '@/lib/api'`

**Architecture et technologies :**

- Framework : Next.js 14 avec App Router
- Pattern : Server Components par défaut (Next.js 14)
- Structure : Séparation claire entre pages (`app/`), composants réutilisables (`components/`), et utilitaires (`lib/`)
- Styling : Classes CSS (à confirmer selon le code)

**Observations supplémentaires :**

✅ **Points forts :**
- Code bien organisé et facile à comprendre
- Séparation claire des responsabilités (pages, composants, API)
- Utilisation des routes dynamiques pour les détails restaurants
- Centralisation des appels API dans `lib/api.js` facilite la maintenance

## Tests fonctionnels (par QA — [Ton Prénom])

Fonctionnalités testées :
- Page d'accueil : liste des restaurants affichée correctement
- Page détail : plats du restaurant affichés
- Route GET /api/restaurants : retourne la liste JSON
- Route GET /api/restaurants/:id : retourne un restaurant par son ID
- Route GET /api/plats : retourne tous les plats
 
Bugs trouvés : aucun / [liste tes bugs]

 ### Synthèse (par CP -- Ibrahima)
**Ce qui fonctionne bien:**
- L'API restaurants
- La page d'accaueil et détails frontend
- Le script de seeding

**Ce qui manque:**
- Pas de gestion d'erreurs visible (si l'API ne répond pas)
- Pas de loader/spinner pendant le chargement des données
- Pas de système de recherche ou de filtres
- Pas de formulaire pour ajouter un restaurant ou un plat (CRUD incomplet)
