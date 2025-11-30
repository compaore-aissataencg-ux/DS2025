Rapport  des Ventes de Champagne
1. Introduction
Ce rapport présente les résultats de l'analyse exploratoire et de la modélisation des ventes mensuelles de champagne. L'objectif était d'identifier la tendance générale des ventes et d'évaluer la pertinence d'un modèle de régression linéaire simple.
2. Préparation des Données
Les données brutes ont été chargées et nettoyées avant l'analyse. Les étapes suivantes ont été réalisées :
 * Chargement : Les données ont été importées à partir d'un fichier source (Excel ou CSV).
 * Nettoyage :
   * Sélection des colonnes pertinentes : "Month" (Mois) et "Sales" (Ventes).
   * Renommage des colonnes en français : Mois et Ventes.
   * Suppression des lignes ne contenant pas de données (valeurs manquantes).
 * Transformation :
   * Conversion de la colonne Mois au format date.
   * Création d'une variable Temps (index numérique 0, 1, 2...) pour faciliter la régression linéaire.
3. Analyse de Tendance (Régression Linéaire)
Un modèle de régression linéaire a été appliqué pour déterminer la direction générale des ventes au fil du temps.
Résultats du Modèle :
 * Pente (Coefficient) : +22.49
   * Interprétation : Les ventes augmentent en moyenne d'environ 22,5 bouteilles par mois sur la période analysée. Cela indique une tendance positive globale.
 * Score R² : 0.0719
   * Interprétation : Le score R² est très faible (proche de 0). Cela signifie que la régression linéaire simple n'explique qu'environ 7,2 % de la variance des ventes. Ce résultat suggère que les ventes sont fortement influencées par d'autres facteurs non capturés par une simple droite, très probablement la saisonnalité (pics de ventes à des périodes précises comme les fêtes).
4. Visualisation
Une tentative de visualisation a été effectuée pour superposer les ventes réelles et la tendance calculée.
 * Le graphique a tracé la courbe des Ventes Réelles.
 * Note technique : Lors de la génération du graphique, le code a signalé que la colonne 'Tendance' était introuvable dans le jeu de données final, empêchant l'affichage de la droite de régression sur le graphique final.
5. Conclusion
L'analyse montre que bien que les ventes de champagne soient en croissance globale (pente positive), un modèle linéaire simple est insuffisant pour prévoir les ventes avec précision (R² faible).
saisonnalité, comme la décomposition saisonnière ou des modèles de séries temporelles plus avancés (ex: SARIMA ou Holt-Winters), car la variation mensuelle est le facteur dominant.
