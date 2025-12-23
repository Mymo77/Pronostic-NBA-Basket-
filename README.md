# Modélisation de Prédiction NBA 🏀

## Objectif du Projet
L'objectif de ce projet est de concevoir un **modèle de machine learning** capable de prédire l’issue des matchs de la NBA en se basant sur les statistiques des feuilles de match (*boxscores*) des 10 dernières saisons.

Pour atteindre cet objectif, j'ai :  
- Développé un outil de **web-scraping personnalisé** pour collecter les données de plus de 12 000 matchs.  
- Agrégé et préparé plusieurs jeux de données pour la modélisation.  
- Testé et itéré sur différents algorithmes pour optimiser la précision des prédictions.  

---

## Partenaire / Stakeholder
Le projet a été réalisé pour **Stat-Ball**, un site d’actualités sportives et de divertissement.  
La plateforme souhaite lancer des compétitions de pronostics et a besoin d’un **modèle interne robuste** servant de référence (*benchmark*) pour les utilisateurs.

---

## Résumé du Projet
- Le meilleur modèle obtenu est un **Gaussian Naive-Bayes (GNB)** avec réduction de dimensionnalité via **PCA**.  
- Entraîné sur les statistiques moyennes des équipes sur les 20 derniers matchs.  
- **Précision obtenue : 63,5 %**, légèrement en dessous du seuil cible de 68 % (victoire moyenne des favoris en NBA).  
- Prochaine étape : intégrer les **données joueurs et statistiques avancées** pour améliorer la précision.  

---

## Table des Matières
1. [Aperçu des Données](#aperçu-des-données)  
2. [Modélisation](#modélisation)  
3. [Résultats](#résultats)  
4. [Prochaines Étapes](#prochaines-étapes)  
5. [Technologies utilisées](#technologies-utilisées)  

---

## Aperçu des Données
- Le dataset final contient des statistiques agrégées par équipe sur des fenêtres de **10, 20 et 30 matchs**.  
- La distribution des données est **approximativement normale**, limitant le besoin de prétraitement lourd.  

### Collecte des données
- Extraction des données de saison régulière des **10 dernières années** via [basketball-reference.com](https://www.basketball-reference.com).  
- Base SQLite structurée avec **3 tables** : informations de match, statistiques joueurs, statistiques équipes.  
- **341 669 observations** et **46 colonnes** couvrant 11 979 matchs.  

### Agrégation des données
- Une moyenne sur 20 matchs offre un bon compromis entre **stabilité et réactivité aux performances récentes**.  
- Limites : pas de données de suivi des joueurs (*player tracking*) et agrégation basée sur l’équipe plutôt que sur les joueurs individuels.  

---

## Modélisation
Algorithmes testés :  
- Régression Logistique  
- K-Nearest Neighbors (KNN)  
- Random Forest (RF)  
- Gaussian Naive-Bayes (GNB)  
- Support Vector Classifier (SVC)  
- Réseaux de Neurones (NN)  

**Modèle de référence (Baseline)** : prédire systématiquement la victoire de l’équipe à domicile (~57,2 % de victoires à domicile).  

### Analyse des erreurs
- Les erreurs sont plus fréquentes **en début de saison** (changements d’effectifs : transferts, draft).  
- Le modèle GNB réduit les faux positifs et détecte mieux les victoires à l’extérieur.  

---

## Résultats
- **Gaussian Naive-Bayes (PCA)** : 63,5 % de précision  
- **Random Forest (Feature Selection)** : 62,8 %  
- **Régression Logistique** : 62,1 %  

**Observations** :  
- Les variables les plus importantes : efficacité au tir, différentiel de rebonds, statistiques défensives.  
- Graphiques recommandés : matrice de confusion, importance des variables, distribution des erreurs par quart de saison.  

---

## Prochaines Étapes
- **Agrégation par joueur** : intégrer les stats individuelles pour ajuster la force d’une équipe.  
- **Ingénierie de caractéristiques avancées** : metrics comme PIE (Player Impact Estimate) ou BPM (Box Plus/Minus).  
- **Modèles d’ensemble** : combiner plusieurs modèles (Boosting/Stacking) pour améliorer la précision.  
- **Données contextuelles** : fatigue, matchs consécutifs, distances de déplacement.  

---

## Technologies utilisées
- **Python** : Pandas, Scikit-Learn, BeautifulSoup, Selenium  
- **SQL** : SQLite  
- **Analyse de données** : PCA, Feature Selection  
- **Visualisation** : Matplotlib, Seaborn
