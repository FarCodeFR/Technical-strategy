# ADR-0003 : Infrastructure et scalabilité

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

Comment absorber les pics de trafic ×10 et suivre l'application en temps réel ?

## 4. Facteurs de décision

- Scalabilité (pics ×10) : …
- Fiabilité : …
- Sécurité : …
- Évolution métier : …
- Maintenabilité (équipe de 6 devs) : …
- Coût : …

## 5. Options envisagées

### Option 1 — Hébergement managé actuel (Firebase / Vercel)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Kubernetes (pods, autoscaling, dashboard temps réel)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Autre approche managée (serverless, conteneurs managés type Cloud Run)

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
