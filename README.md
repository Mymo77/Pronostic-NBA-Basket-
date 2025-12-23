# Modélisation de Prédiction NBA 🏀

## Objectif du Projet
L'objectif de ce projet est de concevoir un **modèle de machine learning** capable de prédire l’issue des matchs de la NBA en se basant sur les statistiques des feuilles de match (*boxscores*) des 10 dernières saisons.

Pour atteindre cet objectif, j'ai :  
- Développé un outil de **web-scraping personnalisé** pour collecter les données de plus de 12 000 matchs.  
- Agrégé et préparé plusieurs jeux de données pour la modélisation.  
- Testé et itéré sur différents algorithmes pour optimiser la précision des prédictions.  

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
4. [Conclusion](#conclusion)  
5. [Prochaines Étapes](#prochaines-étapes)  
6. [Technologies utilisées](#technologies-utilisées)  

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

Traditionnellement, le taux de surprises en NBA se situe entre 28 et 32 %, ce qui signifie que l'équipe favorite l'emporte dans 68 à 72 % des cas. Compte tenu des limitations des données utilisées, l'objectif était d'approcher cette précision.

### Analyse des erreurs
- Les modèles présentent plus d’erreurs en début de saison à cause des changements d’effectifs : blessures, transferts, agents libres, draft.  
- Les erreurs sont moins fréquentes en seconde partie de saison, quand les équipes sont stables.  
- L’analyse de l’erreur moyenne par saison et par quart de saison a montré une précision moyenne d’environ 60 %.  

#### Distribution des erreurs par quart de saison
<img width="1324" height="873" alt="model_error_per_season_quarter" src="https://github.com/user-attachments/assets/d0ad58ba-eeff-4793-b62a-c13549161aaa" />

#### Erreur moyenne par match
<img width="1320" height="853" alt="average_error_per_game" src="https://github.com/user-attachments/assets/d1c9da92-2e73-4836-b1c5-f2d6f51acb24" />



---

## Résultats
- **Gaussian Naive-Bayes (PCA)** : 63,5 % de précision  
- **Random Forest (Feature Selection)** : 62,8 %  
- **Régression Logistique** : 62,1 %  

**Observations** :  
- Les variables les plus importantes : efficacité au tir (eFG%, TS%), différentiel de rebonds (TRB%), points marqués (PTS), statistiques défensives.  
- Graphiques recommandés : matrice de confusion, importance des variables, distribution des erreurs par quart de saison.  

<img width="863" height="545" alt="feat_imp_RF_best" src="https://github.com/user-attachments/assets/31372992-158e-4097-9492-622b647571c0" />


---

## Conclusion
Ce projet a permis de mieux comprendre les dynamiques de victoire en NBA à partir des performances passées des équipes.  
- Le **GNB avec PCA** a été le modèle le plus performant (63,5 %), supérieur à la baseline de 57,2 %.  
- Les indicateurs les plus déterminants sont l’efficacité offensive et le contrôle du rebond.  
- Ces résultats montrent que le machine learning peut capturer des dynamiques au-delà des simples effets contextuels.

---

## Prochaines Étapes
- **Agrégation par joueur** : intégrer les stats individuelles pour ajuster la force d’une équipe.  
- **Ingénierie de caractéristiques avancées** : metrics comme PIE ou BPM.  
- **Modèles d’ensemble** : combiner plusieurs modèles (Boosting/Stacking).  
- **Données contextuelles** : fatigue, matchs consécutifs, distances de déplacement.  

---

## Technologies utilisées
- **Python** : Pandas, Scikit-Learn, BeautifulSoup, Selenium  
- **SQL** : SQLite  
- **Analyse de données** : PCA, Feature Selection  
- **Visualisation** : Matplotlib, Seaborn
