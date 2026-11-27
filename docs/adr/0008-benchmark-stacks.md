# ADR-0008 : Benchmark comparatif de stacks

- **Produit** : Looply
- **Type** : Applicatif
- **Statut** : Proposée
- **Date du statut** : 2026-11-27
- **Auteurs** : Timothé (Tech Lead), Émilie (Architecte / Infra)

> Atelier 3 — trois candidats maximum, sur le périmètre le plus structurant. Critères pondérés et notés : **la pondération est fixée et écrite avant la notation**. Sortie : une recommandation et les conditions dans lesquelles elle serait fausse.

## 1. Contexte

### Périmètre comparé

La **stack backend et l'hébergement** : c'est le choix le plus structurant pour Looply, car il conditionne la tenue des pics de trafic, le coût, la sécurité des données et la capacité à évoluer vers la cible à 3 ans. Le front reste en **Next.js** dans les trois cas (déjà en place, adapté au SEO d'une marketplace).

### Situation actuelle

- Monolithe **Next.js + Firebase** (Auth, Firestore, Storage, Cloud Functions), lancé par un profil non technique en no-code / low-code
- Équipe : 2 développeurs, 1 designer, sans profil DevOps

### Contraintes

- **Pics de trafic ×10** (opérations commerciales, saisonnalité de la mode)
- **Budget limité** : chaque euro d'infra ou d'ops est un euro de moins pour le produit
- **Paiement en ligne** (PSD2) et **géolocalisation** : besoin de données fiables et de requêtes par distance
- **Équipe en croissance** : 2 devs → 6 devs à 1 an → équipe étendue à 3 ans (voir `../Architecture-cible.md`)

### Horizons

- **6 mois** : déjà réalisé (Next.js + Firebase), hors benchmark
- **1 an** : stack à retenir pour la montée en charge et l'arrivée des nouveaux devs
- **3 ans** : la stack choisie doit laisser ouverte la cible microservices

## 2. Parties prenantes

| Rôle | Personne | Intérêt dans la décision |
| ---- | -------- | ------------------------ |
| Tech Lead | Timothé | Une stack que l'équipe maîtrise, cohérente avec la trajectoire monolithe → modulith → microservices |
| Architecte / Infra | Émilie | Une infra qui tient les pics ×10 sans exploitation lourde, et portable vers la cible 3 ans |
| Sécurité / Conformité | Vic | Des données personnelles et de paiement protégées, un contrôle d'accès fiable (RGPD, PSD2) |
| Produit / Business | Julie | Un coût maîtrisé et prévisible, une livraison rapide des fonctionnalités |

## 3. Énoncé du problème

Parmi trois stacks candidates, laquelle répond le mieux aux contraintes de Looply (pics ×10, petite équipe en croissance, budget limité, sécurité) à l'horizon 1 an, tout en préparant la cible à 3 ans ?

## 4. Facteurs de décision — pondération

> ⚠️ Pondération fixée le **27/11/2026**, **avant** la notation (proposition à valider en groupe). Elle n'est plus modifiée ensuite.

| Critère | Poids | Justification du poids |
| ------- | ----: | ---------------------- |
| Scalabilité (pics ×10) | 25 % | Contrainte n°1 du cas : une panne pendant un pic fait perdre des ventes et la confiance des utilisateurs |
| Coût (infra + équipe) | 20 % | Budget de jeune entreprise : le coût d'exploitation pèse directement sur la survie du projet |
| Compétences / adapté à l'équipe (2 → 6 devs) | 20 % | Une stack que l'équipe ne sait pas opérer devient un risque, quelle que soit sa qualité technique |
| Sécurité / conformité | 15 % | Données personnelles, localisation et paiement : obligation légale (RGPD, PSD2), mais en partie déléguée au prestataire de paiement (ADR-0002) |
| Évolutivité vers la cible 3 ans | 10 % | Important mais lointain : on privilégie ce qui fonctionne à 1 an tant que la cible reste ouverte |
| Dépendance fournisseur (lock-in) | 10 % | Risque réel (prix, limites techniques) mais secondaire face à la tenue en charge et au coût |
| **Total** | **100 %** | |

## 5. Options envisagées

### Candidat A — Next.js + Firebase (managé, stack actuelle)

- **Description** : on garde la stack actuelle. Firebase fournit l'authentification, la base NoSQL (Firestore), le stockage des photos et les fonctions serverless ; le front est hébergé en managé.
- ✅ **Avantages** : déjà en place, aucune migration ; montée en charge automatique sans configuration ; aucun serveur à gérer, idéal pour 2 devs ; coût à l'usage, faible au départ ; authentification solide fournie.
- ❌ **Inconvénients** : Firestore (NoSQL) est mal adapté aux données relationnelles et transactionnelles d'une marketplace (commandes, paiements, avis) et limité pour les requêtes complexes ; sécurité reposant sur les règles Firestore, faciles à mal écrire ; coût à la lecture qui grimpe fortement avec le trafic ; forte dépendance à Google, migration coûteuse plus tard.

### Candidat B — Next.js + API Node (NestJS) + PostgreSQL sur conteneurs managés (Docker / Cloud Run)

- **Description** : le backend devient une API Node.js en TypeScript (NestJS), organisée en modules (modulith, architecture hexagonale — ADR-0005), packagée avec Docker et déployée sur des conteneurs managés (Cloud Run ou équivalent). Données dans PostgreSQL managé (avec PostGIS pour la géolocalisation — ADR-0004).
- ✅ **Avantages** : autoscaling automatique sans cluster à gérer ; PostgreSQL adapté aux données relationnelles et aux transactions (commandes, paiements) ; même langage (TypeScript) que le front, donc montée en compétence raisonnable ; conteneurs Docker portables (vers Kubernetes à 3 ans, ou un autre cloud) ; NestJS impose une structure en modules qui prépare l'extraction de microservices.
- ❌ **Inconvénients** : migration depuis Firebase à planifier (données, authentification) ; base PostgreSQL facturée en continu, même sans trafic ; il faut gérer les connexions à la base pendant les pics (pool de connexions) ; plus de code à écrire et à maintenir qu'avec Firebase.

### Candidat C — Next.js + microservices sur Docker + Kubernetes

- **Description** : chaque domaine (annonces, utilisateurs, paiement, messagerie) devient un microservice conteneurisé, orchestré par Kubernetes, derrière une API gateway.
- ✅ **Avantages** : scalabilité maximale et fine (chaque service monte en charge seul) ; contrôle total de l'infrastructure ; portabilité maximale (Kubernetes standard, tous clouds) ; correspond directement à la cible 3 ans.
- ❌ **Inconvénients** : complexité très élevée (réseau, observabilité, cohérence des données entre services) ; exige des compétences DevOps / Kubernetes absentes de l'équipe ; coût fixe du cluster et du temps d'exploitation, disproportionné pour 2 à 6 devs ; ralentit fortement la livraison de fonctionnalités ; architecture prématurée pour une jeune application.

### Notation (1 = faible, 5 = excellent)

| Critère | Poids | A | B | C |
| ------- | ----: | :-: | :-: | :-: |
| Scalabilité (pics ×10) | 25 % | 4 | 4 | 5 |
| Coût | 20 % | 4 | 3 | 1 |
| Compétences / équipe | 20 % | 5 | 4 | 1 |
| Sécurité / conformité | 15 % | 3 | 4 | 3 |
| Évolutivité 3 ans | 10 % | 2 | 4 | 5 |
| Dépendance fournisseur | 10 % | 1 | 4 | 5 |
| **Score pondéré (/5)** | | **3,55** | **3,80** | **3,10** |

Score pondéré = somme (note × poids).
- A = 4×0,25 + 4×0,20 + 5×0,20 + 3×0,15 + 2×0,10 + 1×0,10 = **3,55**
- B = 4×0,25 + 3×0,20 + 4×0,20 + 4×0,15 + 4×0,10 + 4×0,10 = **3,80**
- C = 5×0,25 + 1×0,20 + 1×0,20 + 3×0,15 + 5×0,10 + 5×0,10 = **3,10**

### Justification des notes

- **A — Next.js + Firebase**
  - Scalabilité 4 : autoscaling natif, mais Firestore a des limites d'écriture sur un même document (points chauds possibles pendant un pic).
  - Coût 4 : très faible au départ, mais facturation à la lecture qui grimpe avec le trafic.
  - Compétences 5 : déjà maîtrisé, rien à apprendre.
  - Sécurité 3 : authentification solide, mais toute la protection des données repose sur des règles Firestore faciles à mal configurer.
  - Évolutivité 2 : modèle NoSQL et services propriétaires difficiles à découper en microservices.
  - Dépendance 1 : base, auth, stockage et fonctions tous chez Google ; sortir de Firebase revient à tout migrer.
- **B — API Node + PostgreSQL sur conteneurs managés**
  - Scalabilité 4 : conteneurs qui montent en charge automatiquement ; la base PostgreSQL demande un pool de connexions et éventuellement des réplicas en lecture.
  - Coût 3 : à l'usage pour les conteneurs, mais coût fixe de la base managée.
  - Compétences 4 : TypeScript déjà connu ; SQL et Docker à consolider, apprentissage raisonnable.
  - Sécurité 4 : contrôle d'accès dans l'API, intégrité des données en relationnel, secrets et accès gérés par le cloud.
  - Évolutivité 4 : modulith en modules isolés, conteneurs déjà prêts pour Kubernetes.
  - Dépendance 4 : Docker et PostgreSQL sont des standards ; seul l'hébergement des conteneurs est propre au fournisseur.
- **C — Microservices sur Kubernetes**
  - Scalabilité 5 : scalabilité la plus fine, service par service.
  - Coût 1 : cluster facturé en permanence et besoin d'un profil DevOps dédié.
  - Compétences 1 : aucune expérience Kubernetes dans l'équipe, risque fort de mauvaise exploitation.
  - Sécurité 3 : contrôle total, mais surface d'attaque élevée (réseau entre services, configuration du cluster) sans expertise pour la sécuriser.
  - Évolutivité 5 : c'est la cible elle-même.
  - Dépendance 5 : Kubernetes est standard, déplaçable chez n'importe quel cloud.

## 6. Décision prise et impacts

### Recommandation

**Candidat B — Next.js + API Node (NestJS) + PostgreSQL sur conteneurs managés**, score **3,80 / 5**, pour l'horizon **1 an**.

C'est le meilleur compromis : il tient les pics ×10 sans exploitation lourde (comme A), tout en corrigeant ses deux faiblesses majeures, le modèle NoSQL inadapté aux transactions et la dépendance totale à Firebase. Il prépare la cible 3 ans (modules isolés, conteneurs portables) sans payer dès aujourd'hui la complexité de Kubernetes (C).

À noter : l'écart avec A est faible (0,25). La recommandation est donc sensible aux poids du coût et des compétences, d'où l'importance des conditions ci-dessous.

### Trajectoire

- **6 mois (réalisé)** : Next.js + Firebase.
- **1 an** : migration progressive vers B, module par module. L'authentification Firebase peut être conservée au début pour limiter le risque.
- **3 ans** : extraction des modules les plus sollicités (paiement, recherche, notifications) en microservices sur Kubernetes, quand les conditions de l'ADR-0003 sont réunies.

### Conditions dans lesquelles cette recommandation serait fausse

- **Si l'équipe ne grandit pas** (2 devs au-delà d'un an) : la migration coûterait plus qu'elle ne rapporte → rester sur **A**.
- **Si le coût Firebase reste faible** et qu'aucun besoin relationnel fort n'apparaît (paiement entièrement géré par le prestataire, peu de transactions) : l'avantage de B disparaît → rester sur **A**.
- **Si le budget ne permet pas une base managée** facturée en continu → **A**.
- **Si le trafic ou l'équipe dépasse largement les prévisions** (dizaines de devs, nombreux domaines indépendants, besoins de scalabilité très différents par domaine) → passer directement à **C**.
- **Si l'équipe recrute un profil DevOps** expérimenté sur Kubernetes : la note « compétences » de C remonte, et C redevient compétitif plus tôt.

Ces conditions servent de **conditions de réexamen** de la décision.

### Impacts

- ✅ **Positifs** : données relationnelles fiables pour commandes et paiements ; dépendance fournisseur réduite ; code structuré en modules qui facilite l'arrivée des 6 devs ; chemin clair vers la cible 3 ans.
- ❌ **Négatifs / risques** : chantier de migration depuis Firebase (données, auth) à planifier ; montée en compétence SQL / Docker ; coût fixe de la base ; période de transition avec deux systèmes à maintenir.
- **Impact équipe / budget** : temps de migration à prévoir dans la feuille de route à 1 an ; pas de recrutement DevOps nécessaire avant l'horizon 3 ans.

## Liens

- ADR liés : 0001 (stack technique — s'appuie sur ce benchmark), 0002 (paiement), 0003 (infrastructure), 0004 (géolocalisation), 0005 (architecture hexagonale)
- `../Architecture-cible.md` — équipe et budget par horizon
