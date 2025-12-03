# Rapport d'Analyse : Prédiction des Maladies Cardiaques (UCI Heart Disease)

*Auteur :* Compaoré Aissata
*Date :* 03 Décembre 2025
*Source des données :* Kaggle / UCI Heart Disease Dataset

---

## 1. Introduction
Les maladies cardiovasculaires représentent une cause majeure de mortalité mondiale. L'objectif de ce projet est d'analyser les données cliniques de patients pour identifier les facteurs de risque déterminants et de construire un modèle capable de prédire la présence d'une maladie cardiaque.

Le jeu de données utilisé (UCI Heart Disease) contient des variables démographiques (âge, sexe) et médicales (cholestérol, ECG, douleur thoracique). La variable cible à prédire est **num** (ou target), qui classe la maladie selon 5 niveaux de sévérité :
* *0 :* Absence de maladie (Sain).
* *1, 2, 3, 4 :* Présence de maladie (stades de gravité croissante).

## 2. Méthodologie et Stack Technique

### 2.1 Environnement et Outils
L'analyse a été réalisée en *Python* en utilisant les bibliothèques standards de Data Science :
* *Manipulation :* Pandas, Numpy.
* *Visualisation :* Seaborn, Matplotlib.
* *Machine Learning :* Scikit-learn (pour le pré-traitement et la modélisation).

### 2.2 Pipeline de Préparation des Données
Un pipeline de traitement automatisé a été construit pour garantir la qualité des données avant l'entraînement du modèle :

1.  *Nettoyage :* Suppression des doublons et des identifiants non pertinents (id).
2.  *Imputation des valeurs manquantes :*
    * Variables numériques : Remplacement par la *médiane*.
    * Variables catégorielles : Remplacement par la valeur la plus fréquente (*mode*).
3.  *Transformation :*
    * **Standardisation (StandardScaler) :** Appliquée aux variables numériques (age, chol, trestbps, etc.) pour normaliser les échelles.
    * **Encodage (OneHotEncoder) :** Transformation des variables catégorielles (sex, cp, restecg) en variables binaires.
4.  *Séparation :* Le jeu de données a été divisé en un ensemble d'entraînement (*80%) et un ensemble de test (20%*).

## 3. Analyse Exploratoire des Données (EDA)

L'exploration visuelle a permis de mettre en évidence plusieurs corrélations clés :

### 3.1 Facteurs Physiologiques
* **Dépression ST (oldpeak) :** Les Boxplots montrent une corrélation positive nette. Plus la valeur de oldpeak est élevée, plus le stade de la maladie (target 1 à 4) est avancé. C'est un indicateur de sévérité fiable.
* *Âge :* On observe une prévalence plus forte de la maladie chez les sujets plus âgés ("Seniors") par rapport aux sujets jeunes.

### 3.2 Facteurs Cliniques (Symptômes)
* **Douleur Thoracique (cp) :** L'analyse montre que l'angine "asymptomatique" est paradoxalement la plus fortement liée aux cas positifs de maladie cardiaque.
* **Angine d'effort (exang) :** La présence d'une douleur déclenchée par l'exercice est un discriminateur très puissant. Elle est massivement présente chez les malades et rare chez les sujets sains.

## 4. Modélisation et Résultats

### 4.1 Configuration
* *Modèle :* Classification multi-classes (prédiction des 5 états : 0, 1, 2, 3, 4).
* *Données :* Entraînement sur les données transformées (X_train_prepared).

### 4.2 Performance Globale
Le modèle obtient une *Précision (Accuracy) globale de 52%*.

### 4.3 Analyse Détaillée (Classification Report)
Le détail des scores par classe permet de comprendre les limites actuelles du modèle :

| Classe (Gravité) | Précision | Rappel | Conclusion |
| :--- | :--- | :--- | :--- |
| *0 (Sain)* | *0.77* | *0.86* | *Excellente détection.* Le modèle identifie correctement la majorité des patients sains. |
| *1 (Stade 1)* | 0.22 | 0.23 | Difficulté majeure. Confondu avec les stades 0 ou 2. |
| *2, 3* | ~0.15 | ~0.10 | Très faible détection due au manque de données pour ces classes. |
| *4 (Grave)* | 0.00 | 0.00 | Le modèle échoue à identifier ce stade rare. |

Le score de 52% s'explique par la confusion du modèle entre les différents stades de maladie (ex: prédire un stade 1 alors que c'est un stade 2).

## 5. Conclusion et Perspectives

Cette étude a permis de valider la pertinence de variables comme **oldpeak** et **exang** dans la détection des maladies cardiaques. Si le modèle distingue bien les patients sains des patients malades, il peine à différencier précisément le niveau de gravité (1 vs 2 vs
