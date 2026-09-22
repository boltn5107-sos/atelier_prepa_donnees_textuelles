# Atelier Préparation de Données Textuelles

## Description

Ce projet a pour objectif de préparer un corpus d'avis clients afin de le rendre propre et exploitable pour un modèle de Machine Learning ou de Deep Learning capable de classifier automatiquement le sentiment.

Les avis proviennent de plusieurs sources (site web, application mobile, formulaire de satisfaction, réseaux sociaux, service client) et présentent de nombreux problèmes de qualité : textes vides, doublons, fautes de frappe, majuscules/minuscules incohérentes, caractères spéciaux, emojis, URLs, mentions, hashtags, répétitions de caractères, textes trop courts ou trop longs, valeurs manquantes et classes déséquilibrées.

L'atelier consiste à construire un pipeline complet de nettoyage, de normalisation, de tokenisation et de vectorisation de ces données textuelles.

## Structure du projet

```
atelier_prepa_donnees_textuelles/
│
├── README.md
│
├── notebooks/
│ └── atelier_prepa_donnees_textuelles.ipynb
│
└── data/
├── smart_reviews_raw.csv (données brutes fournies)
├── smart_reviews_cleaned.csv (créé après normalisation)
└── tfidf_matrix.npz (créé après vectorisation)
```

## Étapes réalisées

### Partie 1 – Exploration du corpus

- Chargement du fichier `smart_reviews_raw.csv`.
- Analyse du nombre d'avis, du nombre de colonnes et du type de chaque colonne.
- Détection des valeurs manquantes.
- Identification des types de texte (normal, vide, URL, mention, hashtag, emoji, majuscules, répétitions).
- Mesure de la longueur des textes (minimale, maximale, moyenne, médiane, quartiles).
- Visualisation de la distribution des longueurs.
- Détection des textes vides et des doublons.
- Analyse de l'équilibre des classes et identification de la classe majoritaire.
- Détection des caractères particuliers (emojis, URLs, hashtags, mentions, chiffres, ponctuation répétée).
- Visualisation du nombre d'avis par source et par produit.

### Partie 2 – Nettoyage

- Suppression des lignes avec valeurs manquantes dans le texte.
- Suppression des doublons.
- Suppression des URLs.
- Traitement des mentions (supprimées) et des hashtags (conservés sans le #).
- Nettoyage des espaces multiples.
- Traitement de la ponctuation (réduction des répétitions, suppression des caractères spéciaux).
- Création d'une fonction de nettoyage automatisée.
- Création de la colonne `texte_clean`.
- Vérification par comparaison des colonnes `texte` et `texte_clean`.

### Partie 3 – Tokenisation

- Explication des limites de `split()` pour le NLP.
- Utilisation de NLTK pour la tokenisation.
- Calcul du nombre de tokens par texte, du nombre moyen, du texte avec le plus et le moins de tokens.

### Partie 4 – Normalisation

- Mise en minuscules.
- Conservation des accents (recommandée pour le français).
- Suppression des stop words (avec conservation des négations et intensificateurs).
- Application du stemming avec `FrenchStemmer` de NLTK.
- Reconstruction du texte final dans la colonne `texte_final`.
- Sauvegarde du dataset nettoyé dans `smart_reviews_cleaned.csv`.

### Partie 5 – Découpage Train/Test

- Découpage stratifié avec 80% pour l'entraînement et 20% pour le test.
- Reproductibilité garantie avec `random_state=42`.
- Conservation des proportions de classes dans les deux ensembles.

### Partie 6 – Vectorisation

- Application de la technique **Bag of Words** (CountVectorizer).
- Application de la technique **TF-IDF** (TfidfVectorizer).
- Application de la technique **TF-IDF avec unigrams et bigrams** (ngram_range=(1,2)).
- Comparaison des trois techniques (taille du vocabulaire, shape des matrices).
- Sauvegarde de la matrice TF-IDF retenue dans `tfidf_matrix.npz`.
- Explication des raisons pour lesquelles la vectorisation doit être effectuée après le découpage (fuite de données).

### Partie 7 – Bonus

- Entraînement d'un modèle de régression logistique sur la matrice TF-IDF.
- Évaluation du modèle (accuracy, rapport de classification, matrice de confusion).
- Visualisation de la matrice de confusion.
- Identification des mots les plus importants par classe.
- Création d'une fonction `predire_sentiment()` pour tester sur de nouveaux textes.
- Test de la fonction sur plusieurs exemples.

## Technologies utilisées

- Python 3.8 ou supérieur
- Bibliothèques principales :
  - pandas
  - numpy
  - matplotlib
  - seaborn
  - scikit-learn
  - nltk
  - scipy
  - tqdm

## Installation

1. Cloner le dépôt ou extraire le dossier du projet.

2. Créer un environnement virtuel :

```bash
python -m venv venv
```
