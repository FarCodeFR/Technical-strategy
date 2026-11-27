# ADR-0005 : Organisation interne du code (architecture hexagonale)

- **Produit** : Looply
- **Type** : Applicatif
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Timothé (Tech Lead), Émilie (Architecte / Infra)

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

Comment organiser le code pour que le métier reste isolé et que l'évolution monolithe → modulith → microservices se fasse sans réécriture ?

## 4. Facteurs de décision

- Scalabilité (pics ×10) : …
- Fiabilité : …
- Sécurité : …
- Évolution métier : …
- Maintenabilité (équipe de 6 devs) : …
- Coût : …

## 5. Options envisagées

### Option 1 — Code organisé par couches techniques (pages, API, services)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Architecture hexagonale (métier au centre, ports et adaptateurs)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Découpage par fonctionnalité sans règle d'isolation du métier

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

- ADR liés : 0001 (stack)
