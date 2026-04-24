# Compte-rendu — TP Découverte des Services Web REST

---

## 1. Récapitulatif des opérations effectuées

| Opération              | Verbe  | URL                            | Code obtenu |
|------------------------|--------|--------------------------------|-------------|
| Lire tous les produits | GET    | /produits                      | 200         |
| Lire un produit        | GET    | /produits/1                    | 200         |
| Produit inexistant     | GET    | /produits/999                  | 404         |
| Créer un produit       | POST   | /produits                      | 201         |
| Modifier un produit    | PUT    | /produits/1                    | 200         |
| Supprimer un produit   | DELETE | /produits/2                    | 200         |

---

## 2. Mini-défi cURL (Section 4.8)

### Étape 1 — Ajouter un nouvel utilisateur via POST
```bash
curl -i -X POST http://localhost:3000/utilisateurs \
  -H "Content-Type: application/json" \
  -d '{"nom": "Hichem", "email": "hichem@test.tn"}'
```
**Code de réponse : 201 Created**

### Étape 2 — Lister tous les utilisateurs
```bash
curl -i http://localhost:3000/utilisateurs
```
**Code de réponse : 200 OK**

### Étape 3 — Modifier l'email via PUT
```bash
curl -i -X PUT http://localhost:3000/utilisateurs/3 \
  -H "Content-Type: application/json" \
  -d '{"nom": "Hichem", "email": "hichem.nouveau@test.tn"}'
```
**Code de réponse : 200 OK**

### Étape 4 — Supprimer l'utilisateur via DELETE
```bash
curl -i -X DELETE http://localhost:3000/utilisateurs/3
```
**Code de réponse : 200 OK**

### Étape 5 — Relister les utilisateurs
```bash
curl -i http://localhost:3000/utilisateurs
```
**Code de réponse : 200 OK** — Hichem n'apparaît plus dans la liste.

---

## 3. Questions de réflexion

### Question 1 — Quelle est la différence entre GET et POST ?
GET est utilisé pour **lire** des données existantes sur le serveur, sans les modifier. Il n'envoie pas de corps dans la requête. POST est utilisé pour **créer** une nouvelle ressource : on envoie les données dans le corps (body) de la requête, et le serveur crée un nouvel enregistrement.

### Question 2 — Pourquoi POST renvoie-t-il 201 et pas 200 ?
Le code **200 OK** signifie que la requête a réussi de manière générique. Le code **201 Created** est plus précis : il indique spécifiquement qu'une nouvelle ressource a été créée sur le serveur. Utiliser 201 permet au client de savoir exactement ce qui s'est passé, conformément aux standards HTTP REST.

### Question 3 — Que signifie le code 404 ? Donnez un exemple rencontré dans le TP.
Le code **404 Not Found** signifie que la ressource demandée n'existe pas sur le serveur. Dans le TP, nous avons obtenu un 404 en essayant de lire le produit avec l'id 999 : `curl -i http://localhost:3000/produits/999`. Ce produit n'existant pas dans `db.json`, le serveur a répondu avec 404.

### Question 4 — Que se passe-t-il si vous arrêtez JSON Server puis essayez une requête ?
Si on arrête JSON Server avec Ctrl+C et qu'on tente ensuite une requête, on obtient une **erreur de connexion refusée** (connection refused). cURL affiche `curl: (7) Failed to connect to localhost port 3000: Connection refused`. Il n'y a plus de serveur pour écouter les requêtes, donc la connexion échoue au niveau réseau, avant même qu'un code HTTP soit retourné.

### Question 5 — Pourquoi utilise-t-on JSON plutôt que du texte brut ?
JSON (JavaScript Object Notation) est un format **structuré, lisible et universel**. Contrairement au texte brut, il permet de représenter des objets complexes avec des clés et des valeurs typées (chaînes, nombres, tableaux, booléens). Tous les langages de programmation savent le lire et le produire facilement, ce qui en fait le standard des échanges dans les APIs REST modernes.

---

## 4. État final du fichier db.json

Après toutes les manipulations du TP :
- **Produits restants** : Clavier gamer (id:1), Casque (id:4), Webcam (id:5)
  - Souris (id:2) supprimé en section 4.5
  - Écran (id:3) supprimé en section 5.6
  - Casque (id:4) ajouté en section 4.4
  - Webcam (id:5) ajoutée en section 5.3
  - Clavier (id:1) modifié deux fois : → "Clavier sans fil" (4.5) → "Clavier gamer" (5.4)
- **Utilisateurs** : Amira (id:1), Karim (id:2)
  - Hichem (id:3) créé puis supprimé (sections 4.8 et 5.7)
