# ADR-0006 : Données personnelles, sécurité et conformité (RGPD)

- **Produit** : Looply
- **Type** : Applicatif
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Vic (Sécurité / Conformité), Timothé (Tech Lead)

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

Comment protéger les données des utilisateurs (profil, localisation, messagerie, paiement) et respecter le RGPD ?

## 4. Facteurs de décision

- Scalabilité (pics ×10) : …
- Fiabilité : …
- Sécurité : …
- Évolution métier : …
- Maintenabilité (équipe de 6 devs) : …
- Coût : …

## 5. Options envisagées

### Option 1 — Sécurité fournie par Firebase seule (règles Firestore, Auth)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Renfort applicatif (chiffrement, rôles, journalisation, minimisation des données)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Délégation maximale aux prestataires (paiement, authentification externe)

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

- ADR liés : 0002 (paiement), 0004 (géolocalisation)
