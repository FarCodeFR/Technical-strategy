# ADR-0002 : Service Paiement

- **Produit** : Looply
- **Type** : Applicatif
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Vic (Sécurité) + Timothé (Tech Lead)

## 1. Contexte

Looply est une marketplace entre particuliers : l'acheteur paie en ligne, le vendeur est payé après la vente, et Looply peut prélever une commission. Le paiement passe donc par un tiers (Looply) qui encaisse puis reverse l'argent.

### Contraintes

- **Réglementaires** : conformité **PSD2** (authentification forte du payeur, 3D Secure) ; encaisser pour le compte de tiers impose un statut réglementé ou un prestataire agréé ; vérification d'identité des vendeurs (**KYC**) et lutte anti-blanchiment
- **Sécurité** : aucune donnée de carte ne doit être stockée par Looply (norme **PCI-DSS**)
- **Charge** : supporter des **pics de trafic ×10** sans échec de paiement
- **Équipe** : 2 développeurs aujourd'hui, 6 à 1 an, sans expertise interne du paiement
- **Budget** : limité ; coût à comparer entre frais par transaction et coût de développement / maintenance

### Horizons concernés

- **1 an** : paiement fiable et conforme pour la montée en charge
- **3 ans** : le paiement doit pouvoir devenir un service à part dans l'architecture microservices

## 2. Parties prenantes

| Rôle | Personne | Intérêt dans la décision |
| ---- | -------- | ------------------------ |
| Tech Lead | Timothé | … |
| Architecte / Infra | Émilie | … |
| Sécurité / Conformité | Vic | … |
| Produit / Business | Julie | … |

## 3. Énoncé du problème

Faut-il construire le paiement nous-mêmes ou le déléguer à un prestataire, en restant conforme (PSD2, KYC, PCI-DSS) et capable d'absorber les pics ×10 ?

## 4. Facteurs de décision

- Sécurité / conformité (PSD2, KYC, PCI-DSS) : …
- Scalabilité (pics ×10) : …
- Fiabilité : …
- Évolution métier (commission, reversement aux vendeurs) : …
- Maintenabilité (équipe de 6 devs) : …
- Coût (frais par transaction vs développement) : …
- Délai de mise en place : …

## 5. Options envisagées

### Option 1 — Garder le paiement dans le monolithe

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 2 — Déléguer à un prestataire (Stripe Connect, Mangopay)

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Option 3 — Service de paiement interne dédié

- Description : …
- ✅ Avantages : …
- ❌ Inconvénients : …

### Comparatif

| Facteur | Option 1 | Option 2 | Option 3 |
| ------- | -------- | -------- | -------- |
| Sécurité / conformité | | | |
| Scalabilité | | | |
| Fiabilité | | | |
| Évolution métier | | | |
| Maintenabilité | | | |
| Coût | | | |
| Délai | | | |

## 6. Décision prise et impacts

**Option retenue :** Option X, parce que…

- ✅ Impacts positifs : …
- ❌ Impacts négatifs / risques : …
- Condition de réexamen : …

## Liens

- ADR liés : 0001 (stack), 0003 (infrastructure), 0006 (données personnelles / sécurité)
