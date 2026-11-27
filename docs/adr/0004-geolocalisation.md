# ADR-0004 : Géolocalisation et recherche de proximité

- **Produit** : Looply
- **Type** : Fonctionnel
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Timothé (Tech Lead), Julie (Produit / Business)

## 1. Contexte

- Situation actuelle : …
- Contraintes : …
- Horizons concernés : 1 an … / 3 ans …

## 2. Parties prenantes

| Rôle | Personne | Intérêt dans la décision |
| ---- | -------- | ------------------------ |
| Tech Lead | Timothé | … |
| Architecte / Infra | Émilie | … |
| Sécurité / Conformité | Vic | … |
| Produit / Business | Julie | … |

## 3. Énoncé du problème

Comment proposer une mise en relation géolocalisée entre particuliers (recherche par distance), sans exposer leur adresse exacte ?

## 4. Facteurs de décision

- Scalabilité (pics ×10) : …
- Fiabilité : …
- Sécurité : …
- Évolution métier : …
- Maintenabilité (équipe de 6 devs) : …
- Coût : …

## 5. Options envisagées

### Option 1 — Requêtes géographiques dans Firestore (geohash)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Base dédiée avec index géospatial (PostGIS, Elasticsearch / Algolia)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — API externe (Google Maps / Mapbox) pour le géocodage + recherche maison

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Comparatif

| Facteur | Option 1 | Option 2 | Option 3 |
| ------- | -------- | -------- | -------- |
| Scalabilité | | | |
| Fiabilité | | | |
| Sécurité | | | |
| Évolution métier | | | |
| Maintenabilité | | | |
| Coût | | | |

## 6. Décision prise et impacts

**Option retenue :** Option X, parce que…

- ✅ Impacts positifs : …
- ❌ Impacts négatifs / risques : …
- Condition de réexamen : …

## Liens

- ADR liés : 0001 (stack), 0006 (données personnelles)
