# Looply — Dossier d'architecture (ADR)

> Marketplace de seconde main (vêtements et objets déco) mettant en relation des particuliers, avec **géolocalisation** et **paiement en ligne**.

Ce dépôt documente les **décisions d'architecture** de Looply sous forme d'ADR (_Architecture Decision Record_) : un document court, versionné avec le code, qui enregistre une décision et son contexte, pour que la prochaine équipe comprenne **pourquoi** ce choix a été fait.

- **Cours :** Stratégie technique — M2 Lead Developer Front-End, ECV Nantes (groupe B)
- **Auteurs :** Julie (Produit / Business), Émilie (Architecte / Infra), Vic (Sécurité / Conformité), Timothé (Tech Lead)
- **Dernière mise à jour :** 04/11/2026

---

## Sommaire

1. [Objectif du dépôt](#1-objectif-du-dépôt)
2. [Contexte du projet](#2-contexte-du-projet)
3. [Structure du dépôt](#3-structure-du-dépôt)
4. [Livrables et avancement](#4-livrables-et-avancement)
5. [Registre des ADR](#5-registre-des-adr)
6. [Convention de rédaction d'un ADR](#6-convention-de-rédaction-dun-adr)
7. [Principes d'architecture](#7-principes-darchitecture)
8. [Architecture cible : 6 mois, 1 an, 3 ans](#8-architecture-cible--6-mois-1-an-3-ans)
9. [Workflow de contribution](#9-workflow-de-contribution)
10. [Checklist de restitution](#10-checklist-de-restitution)

---

## 1. Objectif du dépôt

Garder une trace **claire, datée et justifiée** de chaque décision technique structurante :

- Pourquoi cette option plutôt qu'une autre ?
- Quelles contraintes et quels critères ont guidé le choix ?
- Quelles en sont les conséquences, et quand faut-il réexaminer la décision ?

**Règle de base : un ADR = une décision structurante.** Chaque élément demandé (stack, infrastructure, paiement…) dispose de son propre fichier.

---

## 2. Contexte du projet

### Besoins fonctionnels

Géolocalisation · Paiement en ligne · Gestion des profils · Gestion de la recherche · Gestion des annonces · Gestion des disponibilités

### Contraintes

- Projet initié par un profil non technique via du **no-code / low-code** (stack actuelle : Next.js + Firebase)
- **Pics de trafic ×10** à absorber
- Priorisation des tâches nécessaire (ressources limitées)
- Conformité **PSD2** pour le paiement
- Équipe en croissance : 2 devs → 6 devs → équipe étendue

### Critères de décision (_decision drivers_)

Performance · Compétences · Coût global · Support · Disponibilité · Fiabilité · Sécurité · Scalabilité

---

## 3. Structure du dépôt

```text
.
├── README.md                                      # Ce fichier
└── docs/
    ├── adr.md                                     # ADR global : contexte, besoins, options, décision
    ├── Architecture-cible.md                      # Architecture, équipe, budget à 6 mois / 1 an / 3 ans
    └── adr/
        ├── 0001-stack-technique.md                 # ADR-0001
        ├── 0002-service-paiement.md               # ADR-0002
        ├── 0003-infrastructure-kubernetes.md      # ADR-0003
        ├── 0004-geolocalisation.md                # ADR-0004
        ├── 0005-architecture-hexagonale.md        # ADR-0005
        ├── 0006-donnees-personnelles-securite.md  # ADR-0006
        ├── 0007-strategie-de-rendu.md             # ADR-0007
        └── ...
```

**Nommage :** `NNNN-titre-en-kebab-case.md` — numérotation séquentielle sur 4 chiffres, jamais réutilisée.

---

## 4. Livrables et avancement

| Livrable                                        | Fichier                                        | Statut                                                         |
| ----------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------- |
| ADR global (contexte, options, décision finale) | `docs/adr.md`                                  | 🟡 En cours — options 2 et 3 à compléter, décision à rédiger   |
| Architecture cible 6 mois / 1 an / 3 ans        | `docs/Architecture-cible.md`                   | 🟡 En cours — budgets, déclencheurs et cible 3 ans à finaliser |
| ADR-0001 — Choix de la stack technique          | `docs/adr/0001-stack-technique.md` | 🔴 Fichier vide — à rédiger                                    |
| ADR-0002 — Service de paiement                  | `docs/adr/0002-service-paiement.md`            | 🟡 Gabarit posé — à compléter                                  |
| ADR-0003 — Infrastructure / Kubernetes          | `docs/adr/0003-infrastructure-kubernetes.md`   | ⚪ À créer                                                     |
| Restitution finale                              | —                                              | ⚪ Séance 6                                                    |

Légende : 🔴 à faire · 🟡 en cours · 🟢 terminé · ⚪ non démarré

---

## 5. Registre des ADR

Les ADR portent sur les horizons **1 an** et **3 ans**, car les 6 mois sont déjà réalisés. Un ADR est créé pour **chaque élément de décision identifié dans `docs/adr.md`** :

| N°   | Titre | Type | Question à trancher | Options à comparer | Statut |
| ---- | ----- | ---- | ------------------- | ------------------ | ------ |
| 0001 | Choix de la stack technique | Applicatif | Garder, faire évoluer ou remplacer la stack actuelle selon l'horizon (1 an, 3 ans) ? | Next.js + Firebase (monolithe) · Modulith · Microservices | Proposée |
| 0002 | Service de paiement | Applicatif | Construire ou déléguer le paiement (PSD2, pics ×10, équipe de 6 devs) ? | Paiement dans le monolithe · Prestataire (Stripe Connect, Mangopay, PayPal) · Service interne dédié | Proposée |
| 0003 | Infrastructure et scalabilité | Applicatif | Comment absorber les pics ×10 et suivre l'application en direct ? | Hébergement managé actuel · Kubernetes · Autre approche managée | Proposée |
| 0004 | Géolocalisation et recherche de proximité | Fonctionnel | Comment proposer une recherche par distance sans exposer l'adresse exacte ? | Geohash Firestore · Base géospatiale dédiée · API externe + recherche maison | Proposée |
| 0005 | Architecture hexagonale | Applicatif | Comment isoler le métier pour évoluer vers modulith puis microservices sans réécriture ? | Couches techniques · Hexagonale · Découpage par fonctionnalité | Proposée |
| 0006 | Données personnelles, sécurité et RGPD | Applicatif | Comment protéger les données utilisateurs et respecter le RGPD ? | Firebase seul · Renfort applicatif · Délégation aux prestataires | Proposée |
| 0007 | Stratégie de rendu des pages | Applicatif | Quel mode de rendu Next.js par type de page (pics ×10, SEO, fraîcheur) ? | Tout SSR · Tout SSG · Rendu par type de page | Proposée |

> Ajouter une ligne à **chaque nouvel ADR**.


---

## 6. Convention de rédaction d'un ADR

### Statuts

`Proposée` → `À valider` → `Validée` (puis `Remplacée` ou `Dépréciée`)

- **Proposée** : rédaction en cours par l'auteur
- **À valider** : relecture par le groupe
- **Validée** : décision adoptée collectivement

La **date du statut** est mise à jour à chaque changement de statut.

### Types

- **Applicatif** : décision technique (stack, infrastructure, architecture…)
- **Fonctionnel** : décision liée au métier ou au produit (parcours, règles de gestion…)

### Règle d'immutabilité

**Un ADR validé n'est jamais modifié.** Pour changer une décision, on écrit un **nouvel ADR** qui remplace l'ancien :

- le nouvel ADR indique la **date** et le **lien** vers l'ADR remplacé ;
- l'ancien passe au statut `Remplacée` et pointe vers le nouveau (« Remplacée par ADR-XXXX »).

### Gabarit

```markdown
# ADR-NNNN : Titre de la décision

- **Produit** : Looply
- **Type** : Applicatif | Fonctionnel
- **Statut** : Proposée | À valider | Validée | Remplacée par ADR-XXXX | Dépréciée
- **Date du statut** : AAAA-MM-JJ
- **Auteurs** : …

## 1. Contexte

Situation, besoins, contraintes (pics ×10, équipe, budget, conformité…).

## 2. Parties prenantes

Qui est concerné et qui valide (Produit, Architecture / Infra, Sécurité, Tech Lead, devs…).

## 3. Énoncé du problème

La question précise à trancher, en une ou deux phrases.

## 4. Facteurs de décision

Critères de choix : performance, coût, sécurité, scalabilité, compétences, support…

## 5. Options envisagées

1. Option A — description courte
2. Option B — description courte
3. Option C — description courte

| Critère | Option A | Option B | Option C |
| ------- | -------- | -------- | -------- |

## 6. Décision prise et impacts

**Option retenue :** Option X, parce que… (argumentation reliée aux facteurs de décision)

- Impacts positifs : …
- Impacts négatifs / risques : …
- Condition de réexamen : …
```

### Règles de qualité

- **Une décision par fichier**, formulée de façon précise
- **Au moins deux options réelles** comparées, y compris « ne rien changer »
- Décision **justifiée par les critères**, pas par une simple préférence
- Conséquences **négatives assumées** et **condition de réexamen** explicite
- Cohérence avec `Architecture-cible.md` et avec les principes du § 7

---

## 7. Principes d'architecture

- **Un seul style d'architecture par projet**, mais plusieurs **design patterns** combinables selon les besoins.
- **Architecture hexagonale** : le métier est au centre, isolé de tout le reste (base de données, framework, API externes). Il ne dépend que de **ports** (interfaces) que les **adaptateurs** implémentent. Une brique technique peut ainsi être testée ou remplacée sans tout casser, ce qui facilite l'évolution monolithe → modulith → microservices.
- **Stratégie de rendu par type de page** (Next.js) : pages stables (SSG/ISR), fiches annonces (ISR + CDN), pages dynamiques (SSR).

---

## 8. Architecture cible : 6 mois, 1 an, 3 ans

|                          | **6 mois**                                                                       | **1 an**                                                                   | **3 ans**                                              |
| ------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------ |
| **Rôle dans le dossier** | Ce qui est construit maintenant, avec l'équipe et le budget réels (déjà réalisé) | Extractions et renforts prévus, avec leurs **conditions de déclenchement** | **Cible assumée** (plutôt microservices)               |
| **Architecture**         | Monolithe Next.js + Firebase                                                     | Modulith                                                                   | Microservices (gateway, back, front, services)         |
| **Développeurs**         | 2                                                                                | 5 + 1 Lead Dev                                                             | 12 + 1 Lead Dev + 1 Lead Tech                          |
| **Autres rôles**         | 1 designer                                                                       | 1 designer                                                                 | 2 designers, 1 PO (support), 1 Scrum Master, 1 testeur |
| **Salaire**              | 3 000 € brut / pers.                                                             | 1 800 € / pers.                                                            | 1 800 € / pers.                                        |
| **Loyer**                | Aucun                                                                            | 1 500 € (open space)                                                       | 700 € (open space)                                     |
| **Matériel**             | Aucun                                                                            | PC entreprise                                                              | PC entreprise + périphériques sur demande              |
| **Outils**               | Frais de paiement et d'hébergement                                               | Hébergement évolutif selon le nombre d'utilisateurs                        | Hébergement évolutif selon le nombre d'utilisateurs    |

### Questions auxquelles le dossier doit répondre

- **À 1 an :** quelles extractions (ex. paiement, notifications) et quels renforts sont prévus, et **à quelle condition** se déclenchent-ils (seuil de trafic, taille d'équipe, incident, coût) ?
- **À 3 ans :** l'architecture d'aujourd'hui **laisse-t-elle la cible ouverte** ? Quelles décisions prises maintenant (modules découplés, hexagonale, services externalisés) évitent une réécriture ?
- **Pour chaque horizon :** budget, loyer (sans aller trop loin), organisation, nombre de développeurs, salaire brut employeur.

---

## 9. Workflow de contribution

1. **Créer une branche** : `adr/NNNN-titre-court`
2. **Copier le gabarit** (§ 6) dans `docs/adr/NNNN-titre-court.md`
3. **Rédiger** l'ADR avec le statut `Proposée`
4. **Passer le statut à `À valider`** : relecture par au moins un autre membre du groupe (Tech Lead pour la cohérence globale)
5. **Passer le statut à `Validée`** après validation collective (mettre à jour la date du statut)
6. **Mettre à jour** le registre (§ 5) et l'avancement (§ 4)

| Rôle                  | Responsabilité                                                 |
| --------------------- | -------------------------------------------------------------- |
| Tech Lead             | Cohérence des décisions, tenue du registre, restitution finale |
| Architecte / Infra    | ADR stack, infrastructure, scalabilité                         |
| Sécurité / Conformité | PSD2, données personnelles, sécurité des paiements             |
| Produit / Business    | Besoins, coûts, priorisation, impacts métier                   |

---

## 10. Checklist de restitution

- [ ] `docs/adr.md` complet : options 1 à 3 détaillées et **décision finale** renseignée
- [ ] Un ADR rédigé et statué pour **chaque élément** du registre (§ 5)
- [ ] `0001-stack-technique.md` complété
- [ ] `0002-service-paiement.md` complété (option retenue, conséquences, réexamen)
- [ ] ADR infrastructure / Kubernetes créé
- [ ] `Architecture-cible.md` finalisé : budgets, organisation et salaires cohérents sur les 3 horizons
- [ ] Conditions de déclenchement des extractions et renforts à 1 an documentées
- [ ] Cohérence entre l'architecture actuelle et la cible 3 ans justifiée
- [ ] Les 5 axes d'analyse couverts : **scalabilité** (pics ×10), **fiabilité**, **sécurité**, **évolution métier** (paiement), **maintenabilité** (équipe de 6 devs)
- [ ] Registre des ADR à jour et liens entre fichiers vérifiés
- [ ] Orthographe relue (ex. « Kubernetes », « PayPal »)
- [ ] Support de restitution préparé pour la séance 6
