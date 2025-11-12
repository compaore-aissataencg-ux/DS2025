
COMPAORÉ AISSATA
***

# Analyse Statistique Détaillée  
## Dataset : Default of Credit Card Clients (Yeh, I., UCI Machine Learning Repository)

### 1. Présentation du Dataset

- **Source** : I-Cheng Yeh, 2009, UCI Machine Learning Repository ([DOI:10.24432/C55S3H](https://doi.org/10.24432/C55S3H))
- **Objectif** : Prédire le défaut de paiement des clients de cartes de crédit à Taïwan selon diverses caractéristiques socio-démographiques et historiques de paiement.
- **Échantillon** : 30 000 clients
- **Variables** : 23 explicatives, 1 cible (`default payment next month`)
- **Licence** : Creative Commons Attribution 4.0 International (CC BY 4.0)

### 2. Description des Variables Principales

- **LIMIT_BAL** : Montant du crédit accordé (en NT dollars)
- **SEX** : Genre (1 = homme; 2 = femme)
- **EDUCATION** : Niveau d’éducation (1 = études supérieures, 2 = université, 3 = lycée, 4 = autres)
- **MARRIAGE** : Statut marital (1 = marié, 2 = célibataire, 3 = autres)
- **AGE** : Âge du client
- **PAY_0 à PAY_6** : Historique de remboursement mensuel (statut de paiement sur 6 mois)
- **BILL_AMT1 à BILL_AMT6** : Montants des relevés mensuels (NT dollars)
- **PAY_AMT1 à PAY_AMT6** : Montants remboursés par mois (NT dollars)
- **default payment next month** : Cible (1 = défaut de paiement; 0 = pas de défaut)

### 3. Aperçu et Structure

```python
Nombre de lignes : 30 000
Nombre de colonnes : 25

Colonnes principales :
['LIMIT_BAL', 'SEX', 'EDUCATION', 'MARRIAGE', 'AGE', ..., 'default payment next month']

Aperçu des 5 premières lignes :  
(df.head())
```

### 4. Statistiques Descriptives

```python
(df.describe())
```

**Exemple de synthèse** :
- Montant du crédit moyen ≈ 167 000 NT, min : 10 000, max : 1 000 000  
- Âge moyen ≈ 35 ans  
- 36% des clients ont manqué un paiement (target=1)

#### Variables catégoriques

```python
Distribution par genre :
(df['SEX'].value_counts())

Distribution par niveau d’éducation :
(df['EDUCATION'].value_counts())

Distribution par statut marital :
(df['MARRIAGE'].value_counts())

Distribution du défaut de paiement :
(df['default payment next month'].value_counts())
```

### 5. Analyse des Valeurs Manquantes et Outliers

```python
(df.isnull().sum())
```
- **Conclusion** : Pas/peu de valeurs manquantes observées.

Boxplots :
- Permettent de détecter des extrêmes pour LIMIT_BAL, AGE, et les montants mensuels.

### 6. Visualisations

- **Histogrammes** : Distribution des variables numériques (`LIMIT_BAL`, `AGE`, `BILL_AMT1`, ...)
- **Boxplots** : Détection des valeurs aberrantes sur LIMIT_BAL, PAY_0, BILL_AMT1...
- **Heatmap de corrélation** : 

```python
(sns.heatmap(df.corr(), annot=False, cmap='coolwarm'))
```

### 7. Analyse de Corrélations

- **Variables les plus corrélées avec le défaut de paiement** :

```python
Variables les plus corrélées :
(df.corr()['default payment next month'].abs().sort_values(ascending=False).head())
```
- Exemple : Les statuts de paiement récents (PAY_0, PAY_2...) sont les variables les plus prédictives.

### 8. Synthèse

- **Points majeurs** :
  - Taux de défaut ≈ 36%
  - Distribution équilibrée genre et éducation
  - Variables historiques de paiement déterminantes pour la prédiction
  - Peu de valeurs manquantes, dataset prêt à l’usage pour la modélisation.

***

> **Remarque** : Ce rapport Markdown est un squelette expemplatif à compléter avec les véritables sorties chiffrées de vos analyses Python pour chaque section.  

***


