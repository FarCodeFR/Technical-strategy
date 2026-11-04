# ADR — Architecture du projet

## 1. Informations générales

- **Nom du projet :** Looply
- **Auteurs :** Julie, Emilie, Timothé, Vic
- **Date :** 23/10/2026
- **Statut :** En cours

## 2. Contexte et objectifs

### 2.1 Présentation du projet

Une application marketplace qui connecte des particuliers autour de vêtements et d'objets déco de seconde main avec une mise en relation géolocalisée + paiement en ligne.

### 2.2 Besoins et contraintes

- Géolocalisation, Paiement en ligne, Gestion profil, Gestion recherche, Gestion des annonces, Gestion des disponibilités

- Contrainte de temps ou de ressources :

  projet construit par un non-tech via du no-code/low-code
  Pics de trafic x10
  Priorisation des tâches

- 6 mois :
  2 développeur, 1 designer

  Budget [
  Salaire :
  Loyer :
  ]

- 1 ans :
  6 développeur, 1 designer

- 3 ans :

### 2.3 Décision drivers

- Performance
- Compétences
- Coût en général
- Support
- Disponibilité
- Fiabilitié
- Sécurité
- Scalabilité

## 2.4 Options considérées

Choix 1 : Stack actuelle : Next.js + Firebase

Choix 2 : Kubernetest via des pods pour gérer les pics d'utilisateur et avoir un dashboard sur les stats en directs de l'application

Choix 3 : Stripe ou Paypale pour ne pas à avoir la partie paiement à construire et à le gérer

## 2.5 Décision

Choix final :
