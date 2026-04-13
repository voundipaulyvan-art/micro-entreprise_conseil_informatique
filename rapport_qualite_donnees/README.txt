# Base Clients d'une Micro-entreprise de Conseil Informatique

---

## Description

Ce projet porte sur l'analyse, le nettoyage et l'harmonisation d'une base de données clients
d'une micro-entreprise de conseil informatique.

Le dataset initial contenait 500 enregistrements avec de nombreuses anomalies volontairement
introduites : erreurs d'harmonisation, incohérences, valeurs manquantes cachées et doublons métier.

L'objectif était d'améliorer la qualité des données pour les rendre exploitables et fiables
pour des analyses métier.

---

## Compétences démontrées

- Profiling et exploration de données avec Pandas
- Détection de valeurs manquantes, doublons et anomalies
- Nettoyage et harmonisation de données (casse, formats, encodage)
- Conversion de types (texte → numérique, texte → datetime)
- Détection d'incohérences métier
- Calcul d'un score de qualité multi-dimensionnel
- Automatisation via des fonctions Python réutilisables
- Analyse de l'impact métier des données de mauvaise qualité

---

## Technologies utilisées

| Outil       | Usage                              |
|-------------|-------------------------------------|
| Python 3.12 | Langage principal                  |
| Pandas      | Manipulation et nettoyage des données |
| Regex (re)  | Validation des emails              |
| Jupyter     | Environnement de développement     |

---

## Structure du projet

```
qualite-donnees/
│
├── README.md
├── data/
│   ├── BDD_tp_qualite.csv        ← Dataset brut (500 lignes, 10 colonnes)
│   └── dataset_nettoye.csv       ← Dataset nettoyé (367 lignes)
├── notebooks/
│   └── qualite_donnees.ipynb     ← Notebook principal avec tout le code
└── rapport/
    └── rapport_qualite.pdf      ← Rapport de qualité complet
```

---

## Anomalies détectées

| Type d'anomalie              | Nombre | Description                                  |
|------------------------------|--------|----------------------------------------------|
| Emails invalides             | 130    | Espaces dans l'email ou absence du @         |
| Doublons métier (email)      | 133    | Même email enregistré plusieurs fois         |
| Pays non harmonisés          | 255    | Ex : france / France / FR pour le même pays  |
| Dates corrompues             | 500    | date_naissance contient des masques de format|
| Formats de dates mixtes      | 3      | dernier_contact en 3 formats différents      |
| CA non numérique             | ~200   | Symbole €, espaces dans les chiffres         |
| Incohérences métier          | ~12    | CA > 0 avec nb_projets = 0                   |

---

## Corrections appliquées

- **Pays** : harmonisation via dictionnaire de mapping (9 variantes → 4 codes ISO)
- **Noms/Prénoms** : uniformisation de la casse avec str.title()
- **Emails** : suppression des espaces et mise en minuscules
- **Code postal** : suppression des espaces parasites (75 000 → 75000)
- **dernier_contact** : conversion en datetime avec pd.to_datetime()
- **chiffre_affaires_total** : suppression du symbole € et conversion en float
- **date_naissance** : colonne entièrement corrompue → remplacée par NaT
- **Doublons** : suppression des doublons métier (conservation de la 1ère occurrence)

---

## Score de qualité

| Dimension    | Score  | Description                                      |
|--------------|--------|--------------------------------------------------|
| Complétude   | 97.0%  | % de valeurs non nulles                          |
| Validité     | 76.9%  | % d'emails valides ET pays au format ISO         |
| Cohérence    | 97.5%  | % de lignes sans incohérence métier              |
| **GLOBAL**   | **90.35%** | Moyenne des 3 dimensions                    |

> En entreprise, un score inférieur à 70% indique des données non fiables.
> Un score supérieur à 90% est considéré comme acceptable.

---

## Statistiques du dataset nettoyé

- **Clients uniques** : 367 (après suppression de 133 doublons)
- **Chiffre d'affaires total** : 3 008 399 €
- **CA moyen par client** : 8 197 €
- **Nombre moyen de projets** : 9.9 par client
- **Répartition géographique** :
  - France (FR) : 129 clients (35.1%)
  - Algérie (DZ) : 81 clients (22.1%)
  - Maroc (MA) : 79 clients (21.5%)
  - Tunisie (TN) : 78 clients (21.3%)

---

## Leçon clé

> **"Garbage In, Garbage Out"** — Une mauvaise donnée en entrée produit
> une mauvaise analyse en sortie. La qualité des données est le socle
> de toute décision métier fiable.

---

## Auteur

**VOUNDI ABESSOLO Paul Yvan Kheran**
Étudiant en Data / Informatique
[Email: voundipaulyvan@gmail.com]
