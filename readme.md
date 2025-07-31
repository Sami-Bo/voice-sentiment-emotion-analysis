# Projet Synthèse Audio - Pour GitHub
Ce dépôt regroupe les notebooks Jupyter utilisés dans le cadre du projet d’analyse des émotions et sentiments à partir de données audio.

---

## Contenu

Le dossier contient plusieurs notebooks qui couvrent différentes étapes du projet audio :

- **1_audio_dataset_cleaner.ipynb** *(data preprocessing)* :  
  Ce notebook convertit automatiquement les fichiers vidéo `.mp4` en fichiers audio `.wav` pour les dossiers **train**, **test** et **dev**.  
  Il vérifie l’existence des dossiers sources, crée les dossiers de sortie si nécessaire, liste les fichiers `.mp4` et utilise `ffmpeg` pour effectuer la conversion.  
  Il affiche un retour sur la réussite ou l’échec de chaque conversion.

- **2_extraction_caracteristiques.ipynb** *(feature extraction)* :  
  Ce notebook traite l’extraction des caractéristiques audio et la préparation des données pour l’analyse émotionnelle.  
  Il commence par charger un fichier CSV contenant les étiquettes d’émotions et les énoncés correspondants,  
  puis sélectionne les colonnes pertinentes et nettoie les données (suppression des valeurs manquantes).  

  Ensuite, il utilise la bibliothèque OpenSMILE pour extraire des descripteurs audio (fonctionnels du set ComParE 2016) à partir des fichiers `.wav` correspondants.  
  Les caractéristiques extraites sont mises en correspondance avec les émotions associées via un `LabelEncoder`.  

  Pour réduire la dimensionnalité des données audio, il applique une Analyse Discriminante Linéaire (LDA) adaptée au nombre d’émotions et de caractéristiques.  
  Le notebook affiche ensuite les caractéristiques réduites pour un sous-ensemble d’échantillons audio,  
  puis calcule et affiche la moyenne des caractéristiques réduites par émotion pour visualiser la séparation des classes.

- **3_modele_apprentissage.ipynb** : Entraînement et évaluation de plusieurs modèles pour la reconnaissance des émotions et sentiments à partir des caractéristiques audio.  
  Ce notebook charge les fichiers CSV des jeux de données **train**, **dev** et **test** contenant les features extraites (principalement des MFCCs) ainsi que les labels **Emotion** et **Sentiment**.  

  Le notebook effectue les étapes suivantes :  
  - Chargement et fusion des données des différents dossiers.  
  - Sélection des colonnes MFCC (13 coefficients) comme features principales.  
  - Standardisation des données.  
  - Séparation stratifiée en ensembles d’entraînement et de test.  
  - Application d’un oversampling avec `RandomOverSampler` pour équilibrer les classes.  
  - Entraînement et comparaison de plusieurs modèles classiques de machine learning :  
    - Régression logistique  
    - Forêt aléatoire (Random Forest)  
    - Gradient Boosting  
    - K plus proches voisins (KNN)  
    - Arbre de décision  
    - Naïve Bayes  
    - Perceptron multi-couches (MLP)  
    - AdaBoost  
  - Évaluation de chaque modèle avec la précision et rapport de classification.  
  - Sélection du meilleur modèle selon la précision obtenue.  

  En plus, le notebook propose une section dédiée à l’entraînement de modèles profonds (Deep Learning) basés sur des réseaux récurrents :  
  - Prétraitement des données MFCC en format 3D (échantillons, timesteps, features) pour LSTM/GRU.  
  - Encodage des labels en one-hot.  
  - Oversampling adapté pour les données séquentielles.  
  - Construction de réseaux LSTM ou GRU avec couches de normalisation, dropout, et dense.  
  - Utilisation d’early stopping pour éviter le surapprentissage.  
  - Évaluation des modèles profonds sur les jeux de test.  

  Enfin, le notebook inclut également un modèle combiné CNN + LSTM pour exploiter la structure temporelle des MFCCs, avec :  
  - Couches Conv1D et MaxPooling pour extraire les motifs locaux.  
  - Couche LSTM pour capturer la dynamique temporelle.  
  - Couche dense finale pour la classification multi-classes.  
  - Entraînement et évaluation pour les deux tâches Emotion et Sentiment.  

  Ce notebook offre ainsi un panorama complet des approches classiques et profondes pour l’analyse émotionnelle audio, permettant de comparer leurs performances sur les mêmes données prétraitées.
  
- **capturer_voix.ipynb** : Notebook Python interactif permettant de capturer des données vocales en temps réel avec reconnaissance multilingue, détection de commandes vocales d'arrêt personnalisées selon la langue, et extraction de caractéristiques audio avancées via OpenSMILE.

- **kaggle_model_use.ipynb** et autres notebooks liés aux datasets Kaggle, où différents modèles ont été testés.  
- **meld_dl_autres.ipynb**, **ravdess_dp_xgboost.ipynb**, **ravdess_model_use.ipynb** : Notebooks spécifiques pour les datasets MELD, RAVDESS, etc., avec exploration et expérimentation de plusieurs modèles d’apprentissage.
---

## Description du projet

Ce projet vise à construire un modèle audio performant en utilisant plusieurs datasets (MELD, RAVDESS, etc.).  
Différentes approches et modèles ont été testés afin d'optimiser la reconnaissance et l'analyse audio.

---

## Organisation
  
- Les datasets lourds et fichiers temporaires ne sont pas inclus dans ce dépôt.  
- Pour reproduire les résultats, il faudra exécuter les notebooks dans l'ordre.

---

## Pour contribuer ou utiliser ce dépôt

1. Clonez ce dépôt :  
```bash
git clone https://github.com/Sami-Bo/voice-sentiment-emotion-analysis.git
