# ADR-0001 : Choix de la stack technique

- **Produit** : Looply
- **Type** : Applicatif
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Timothé (Tech Lead), Émilie (Architecte / Infra)

## 1. Contexte

### Situation actuelle (6 mois — déjà réalisé)

- Monolithe Next.js + Firebase, construit au départ par un profil non technique (no-code / low-code)
- Équipe : 2 développeurs, 1 designer

### Contraintes

- Pics de trafic ×10
- Budget et équipe (voir `../Architecture-cible.md`)
- Paiement en ligne (PSD2) et géolocalisation
- Évolution de l'équipe : 2 → 6 → équipe étendue

### Horizons concernés

- **1 an** : …
- **3 ans** : …

## 2. Parties prenantes

| Rôle | Personne | Intérêt dans la décision |
| ---- | -------- | ------------------------ |
| Tech Lead | Timothé | … |
| Architecte / Infra | Émilie | … |
| Sécurité / Conformité | Vic | … |
| Produit / Business | Julie | … |
| Équipe de développement | — | … |

## 3. Énoncé du problème

Faut-il garder, faire évoluer ou remplacer la stack actuelle (Next.js + Firebase) pour tenir les horizons 1 an et 3 ans ?

## 4. Facteurs de décision

- **Scalabilité** (pics ×10) : …
- **Fiabilité / disponibilité** : …
- **Sécurité** : …
- **Évolution métier** (paiement, nouvelles fonctionnalités) : …
- **Maintenabilité** (équipe de 6 devs) : …
- **Coût** : …
- **Compétences de l'équipe** : …
- **Support / communauté** : …

## 5. Options envisagées

### Option 1 — Garder le monolithe Next.js + Firebase

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Modulith (monolithe découpé en modules)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Microservices

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
| Compétences | | | |

## 6. Décision prise et impacts

### Option retenue

**Option X**, parce que… (relier aux facteurs de décision)

### Trajectoire

- **1 an** : … (extractions prévues et conditions de déclenchement)
- **3 ans** : … (cible assumée, ce qu'il faut garder ouvert dès maintenant)

### Impacts

- ✅ Positifs : …
- ❌ Négatifs / risques : …
- Impact équipe / budget : …

### Condition de réexamen

…

## Liens

- `../adr.md` — note de cadrage
- `../Architecture-cible.md` — équipe et budget par horizon
- ADR liés : 0002 (paiement), 0003 (infrastructure)
