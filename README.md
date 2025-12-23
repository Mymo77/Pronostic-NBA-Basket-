Modélisation de Prédiction NBA
Par Luke DiPerna
Août 2023
Objectif du Projet
L'objectif de ce projet est de concevoir un modèle d'apprentissage automatique (Machine Learning) capable de prédire avec précision l'issue des matchs de la NBA en s'appuyant sur les statistiques des feuilles de match (boxscores) des 10 dernières saisons.
Pour mener à bien ce projet, j'ai :
Développé un outil de web-scraping personnalisé pour collecter les données de plus de 12 000 matchs.
Agrégé et traité plusieurs jeux de données pour les préparer à la modélisation.
Évalué et itéré sur différents algorithmes pour optimiser la précision des prédictions.
Partenaire / Stakeholder
Le commanditaire de ce projet est Stat-Ball, un site d'actualités sportives et de divertissement. La plateforme souhaite lancer des compétitions de pronostics et a besoin d'un modèle interne robuste servant de référence (benchmark) pour les utilisateurs.
Résumé du Projet
Le meilleur modèle de machine learning obtenu est un Naive-Bayes Gaussien (GNB). Ce modèle a été entraîné sur les statistiques moyennes des équipes sur les 20 derniers matchs, avec une réduction de dimensionnalité via une Analyse en Composantes Principales (PCA). Il affiche une précision de 63,5 %. Bien que ce score soit encourageant, il reste en dessous du seuil cible de 68 %, qui correspond statistiquement au taux de victoire des favoris en NBA. L'ajout de données sur les joueurs et de statistiques avancées constitue la prochaine étape pour franchir ce palier.
Table des Matières
Aperçu des Données
Modélisation
Résultats
Prochaines Étapes
Aperçu des Données
Le jeu de données final comprend des statistiques agrégées par équipe sur des fenêtres de 10, 20 et 30 matchs. Les données présentent une distribution normale, limitant ainsi le besoin de prétraitement lourd.
Collecte des Données
J'ai extrait l'ensemble des données de saison régulière des 10 dernières années via basketball-reference. Le scraper web (disponible sur mon profil GitHub) a permis de construire une base de données SQLite structurée comme suit :
3 tables : informations de match, statistiques joueurs, statistiques équipes.
341 669 observations et 46 colonnes sur 11 979 matchs.
Agrégation des Données
L'enjeu majeur était la "réactivité" des données. Une moyenne sur trop peu de matchs est sensible aux valeurs aberrantes, tandis qu'une moyenne sur une période trop longue ne reflète plus l'état de forme actuel. Mes tests ont démontré que l'agrégation sur 20 matchs offrait le meilleur compromis entre stabilité et performance.
Limites des Données
Absence de données de suivi de mouvement (player tracking).
Agrégation basée sur l'équipe et non sur les joueurs individuels (ne prend pas directement en compte l'absence d'une star sur un match précis).
Modélisation
J'ai testé une large gamme d'algorithmes de classification binaire :
Régression Logistique
K-Nearest Neighbors (KNN)
Random Forest (RF)
Gaussian Naive-Bayes (GNB)
Support Vector Classifier (SVC)
Réseaux de Neurones (NN)
Modèle de Référence (Baseline)
Le modèle de référence consiste à prédire systématiquement la victoire de l'équipe à domicile. En NBA, l'avantage du terrain est réel : l'équipe à domicile gagne environ 57,2 % du temps.
Processus et Analyse d'Erreur
L'analyse montre que les erreurs de prédiction sont plus fréquentes en début de saison. Cela s'explique par les changements d'effectifs durant l'intersaison (draft, transferts) que les modèles basés sur les moyennes historiques mettent du temps à intégrer.
[Graphique : Distribution de l'erreur par quart de saison]
Résultats
Voici une analyse des performances des meilleurs modèles :
Gaussian Naive-Bayes (PCA) : 63,5 % de précision.
Random Forest (Feature Selection) : 62,8 % de précision.
Régression Logistique : 62,1 % de précision.
Le modèle GNB avec PCA s'est distingué par sa capacité à réduire les faux positifs (prédictions de victoires à domicile erronées), offrant une meilleure détection des victoires à l'extérieur par rapport aux autres modèles.
[Graphique : Matrice de confusion du modèle GNB]
L'importance des variables (Feature Importance) souligne que l'efficacité au tir, le différentiel de rebonds et les statistiques défensives sont les prédicteurs les plus solides de la victoire.
[Graphique : Importance des variables - Random Forest]
Prochaines Étapes
Pour atteindre l'objectif de 68 % de précision, les axes d'amélioration sont les suivants :
Agrégation par Joueur : Intégrer les statistiques individuelles pour ajuster automatiquement la force d'une équipe en cas de blessure ou de transfert d'un joueur clé.
Ingénierie de Caractéristiques Avancées : Inclure des métriques comme le PIE (Player Impact Estimate) ou le BPM (Box Plus/Minus).
Modèles d'Ensemble : Combiner les prédictions de plusieurs modèles (Boosting/Stacking) pour capturer des nuances que les modèles individuels ignorent.
Données Contextuelles : Ajouter des variables sur la fatigue (matchs en back-to-back) et les distances de déplacement.
Technologies utilisées
Python (Pandas, Scikit-Learn, BeautifulSoup, Selenium)
SQL (SQLite)
Analyse de données (PCA, Feature Selection, Matplotlib/Seaborn)
