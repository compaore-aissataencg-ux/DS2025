# Rapport – Classification de la qualité du vin blanc par K-plus proches voisins (KNN)
# Fait par COMPAORÉ AISSATA
## Introduction

L’objectif de ce projet est de modéliser la qualité du vin blanc portugais à partir de tests physico-chimiques à l’aide d’un algorithme de classification supervisée, le K-plus proches voisins (KNN).

## 1. Chargement et exploration des données

- Les données sont issues de l’UCI Machine Learning Repository, comportant 4898 échantillons et 12 variables, dont la cible *quality* (score de 0 à 10).
- Les variables d’entrée sont quantitatives (ex : acidité, sucre résiduel, densité).
- Il n’y a pas de valeurs manquantes.
- **Résumé des qualités de vin :**

```
6    2198
5    1457
7     880
8     175
4     163
3      20
9       5
Name: quality, dtype: int64
```

- Les classes sont déséquilibrées : la grande majorité des vins sont "5", "6" ou "7".


## 2. Prétraitement et visualisation

- Transformation binaire de la variable cible possible : =mauvais (0), >5=bon (1).[^11_1]
- Exploration par boxplots et matrice de corrélation pour repérer les variables discriminantes.
- Visualisation des distributions et des corrélations (boîtes à moustaches, heatmap).


## 3. Séparation du jeu de données

- Découpage en :
    - `Xa`, `Ya` : apprentissage
    - `Xv`, `Yv` : validation
- La fonction `train_test_split` est utilisée avec un stratifié pour conserver le déséquilibre des classes.


## 4. Modélisation KNN

- Pour différentes valeurs de $k$ (impaires de 1 à 35), apprentissage du classifieur KNN et calcul du taux d’erreur sur jeu d’entraînement et de validation.
- Boucle de recherche du k optimal :

```python
for ind, k in enumerate(k_vector):
    clf = KNeighborsClassifier(n_neighbors=k)
    clf.fit(Xa, Ya)
    Ypred_train = clf.predict(Xa)
    error_train[ind] = np.mean(Ypred_train != Ya)
    Ypred_val = clf.predict(Xv)
    error_val[ind] = np.mean(Ypred_val != Yv)
```

- Recherche du k optimal avec :

```python
err_min, ind_opt = error_val.min(), error_val.argmin()
k_star = k_vector[ind_opt]
```


## 5. Standardisation

- Les données sont standardisées (`StandardScaler`) car KNN est sensible aux échelles.
- Transformation appliquée sur les jeux d’apprentissage et de validation.


## 6. Analyse des performances

- Évolution des taux d’erreurs en fonction de k, visualisés par une courbe.
- Sélection du k qui minimise l’erreur de validation.
- Discussion du surapprentissage si l’erreur train est très inférieure à l’erreur val.


## Conclusion

- Le meilleur k offre un compromis entre biais et variance.
- La standardisation améliore les performances du KNN.
- L’approche KNN donne des résultats corrects sur ce jeu de données, mais son efficacité dépend du prétraitement et de la distribution des classes.
- Possibilités d’amélioration : analyse d’autres modèles, sélection de variables, gestion du déséquilibre des classes.

***

