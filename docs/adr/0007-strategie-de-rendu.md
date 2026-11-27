# ADR-0007 : Stratégie de rendu des pages

- **Produit** : Looply
- **Type** : Applicatif
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

Quel mode de rendu Next.js utiliser pour chaque type de page afin de tenir les pics ×10, le SEO et la fraîcheur des annonces ?

## 4. Facteurs de décision

- Scalabilité (pics ×10) : …
- Fiabilité : …
- Sécurité : …
- Évolution métier : …
- Maintenabilité (équipe de 6 devs) : …
- Coût : …

## 5. Options envisagées

### Option 1 — Tout en SSR

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Tout en statique (SSG) + client

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Rendu par type de page : SSG/ISR (pages stables), ISR + CDN (annonces), SSR (pages dynamiques)

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

- ADR liés : 0001 (stack), 0003 (infrastructure)
