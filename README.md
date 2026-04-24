# TP REST — Découverte des Services Web REST

Ce dépôt contient les livrables du TP REST réalisé avec **JSON Server**.

## Contenu du dépôt

| Fichier | Description |
|---|---|
| `db.json` | Base de données JSON finale après toutes les manipulations |
| `TP_REST_Collection.postman_collection.json` | Collection Postman exportée (v2.1) |
| `compte-rendu.md` | Compte-rendu : réponses aux questions, commandes cURL et codes HTTP |
| `TP_REST.pdf` | Sujet du TP fourni par le professeur |

## Lancer le serveur localement

```bash
# Installer JSON Server
npm install -g json-server@0.17.4

# Démarrer le serveur
json-server --watch db.json --port 3000
```

L'API sera disponible sur :
- `http://localhost:3000/produits`
- `http://localhost:3000/utilisateurs`

## Ressources testées

| Verbe  | URL               | Action                  | Code |
|--------|-------------------|-------------------------|------|
| GET    | /produits         | Lire tous les produits  | 200  |
| GET    | /produits/1       | Lire un produit         | 200  |
| GET    | /produits/999     | Produit inexistant      | 404  |
| POST   | /produits         | Créer un produit        | 201  |
| PUT    | /produits/1       | Modifier un produit     | 200  |
| DELETE | /produits/3       | Supprimer un produit    | 200  |
