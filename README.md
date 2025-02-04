# 🔍 Analyse et Modélisation des Maladies Cardiovasculaires

## 📌 Présentation du Dataset
Le dataset utilisé provient de Kaggle et se concentre sur la **prédiction des maladies cardiovasculaires** à partir de plusieurs facteurs de risque collectés lors d'examens médicaux.

🔗 **Lien du dataset Kaggle** : [Cardiovascular Disease Dataset](https://www.kaggle.com/datasets/sulianova/cardiovascular-disease-dataset)

## 🏥 Contexte : Les Maladies Cardiovasculaires (MCV)
Les MCV affectent le cœur et les vaisseaux sanguins. Elles sont souvent associées à des facteurs de risque tels que :
- **Hypertension** (pression artérielle élevée)
- **Taux élevé de cholestérol**
- **Obésité**
- **Mode de vie** (tabac, alcool, manque d'activité physique)

### 🎯 **Objectif du projet**
Prédire si un individu est atteint d'une maladie cardiovasculaire (`cardio = 1`) en fonction des caractéristiques médicales et des habitudes de vie.

---

## 📊 Structure des Données

Le dataset contient **3 types de variables** :

### **1️⃣ Informations objectives (métriques factuelles)**
| **Feature** | **Description** | **Type** |
|------------|---------------|----------|
| `age` | Âge en jours (à convertir en années) | Entier |
| `height` | Taille (cm) | Entier |
| `weight` | Poids (kg) | Flottant |
| `gender` | Sexe (1 : Femme, 2 : Homme) | Catégorique |

### **2️⃣ Résultats des examens médicaux**
| **Feature** | **Description** | **Type** |
|------------|---------------|----------|
| `ap_hi` | Pression artérielle systolique (haute) | Entier |
| `ap_lo` | Pression artérielle diastolique (basse) | Entier |
| `cholesterol` | 1 : Normal, 2 : Élevé, 3 : Très élevé | Catégorique |
| `gluc` | 1 : Normal, 2 : Élevé, 3 : Très élevé | Catégorique |

### **3️⃣ Informations subjectives (habitudes de vie)**
| **Feature** | **Description** | **Type** |
|------------|---------------|----------|
| `smoke` | Fumeur (0 : Non, 1 : Oui) | Binaire |
| `alco` | Consommation d'alcool (0 : Non, 1 : Oui) | Binaire |
| `active` | Activité physique régulière (0 : Non, 1 : Oui) | Binaire |

### **🎯 Variable cible : Présence d'une maladie cardiovasculaire**
| **Feature** | **Description** | **Type** |
|------------|---------------|----------|
| `cardio` | 0 : Pas de maladie, 1 : Présence d'une MCV | Binaire |

---

## 🔎 **Analyse Descriptive**

### 📂 **1. Exploration des données**
- Vérification du dataset (`df.head()`, `df.info()`)
- Détection des valeurs manquantes et anomalies (`df.describe()`)

### 📊 **2. Visualisation des données**
- **Histogrammes** : Répartition des âges, poids, taille.
- **Boxplots** : Identifier les valeurs extrêmes de pression artérielle.
- **Matrice de corrélation** : Vérifier les relations entre les variables.

### 🏥 **3. Relations entre facteurs et maladie cardiovasculaire**
- Comparer la pression artérielle entre individus atteints (`cardio=1`) et non atteints (`cardio=0`).
- Analyser l’impact du **tabagisme, alcool, et activité physique** sur la présence des MCV.

---

## ⚙️ **Préparation des Données**

### ✅ **1. Nettoyage**
- Supprimer ou corriger les valeurs aberrantes (`ap_hi > 200` ou `ap_lo < 50`).
- Convertir `age` en années.

### 🔢 **2. Feature Engineering**
- Calcul de l'**IMC** : `df['bmi'] = df['weight'] / ((df['height'] / 100) ** 2)`

### 🔄 **3. Encodage et normalisation**
- Transformer `cholesterol` et `gluc` en variables numériques.
- Normaliser les variables continues (âge, pression, IMC).

### 📌 **4. Division des données**
Les données sont divisées en deux ensembles : un ensemble d'entraînement (80%) pour ajuster le modèle et un ensemble de test (20%) pour évaluer sa performance sur des données inédites.  
Cette séparation permet de s'assurer que le modèle ne surapprend pas sur les données d'entraînement et qu'il généralise bien aux nouveaux patients.  

## 🤖 **5. Modélisation**

### 🔍 1. Choix des modèles
Plusieurs modèles de classification peuvent être testés pour prédire la présence d'une maladie cardiovasculaire :
- **Régression Logistique** : Facile à interpréter et rapide à entraîner.
- **Arbres de décision** : Permet d'obtenir des règles de classification explicites.
- **Forêts aléatoires et XGBoost** : Modèles plus puissants offrant de meilleures performances grâce à l'agrégation d'arbres.

### 📊 2. Validation croisée et évaluation
Pour évaluer la performance des modèles et éviter l'overfitting, une validation croisée est utilisée. L'AUC (Area Under the Curve) est une métrique clé permettant d'évaluer la capacité du modèle à discriminer les patients atteints ou non d’une maladie cardiovasculaire.

### ⚡ 3. Optimisation des hyperparamètres
L'optimisation des hyperparamètres est réalisée à l’aide de `GridSearchCV` pour tester plusieurs configurations et choisir celle offrant la meilleure performance. Les hyperparamètres clés peuvent inclure le nombre d'arbres dans une forêt aléatoire, la profondeur maximale des arbres et le critère de sélection des divisions.

### 📈 4. Évaluation finale
Une fois le meilleur modèle sélectionné, il est testé sur l’ensemble de test indépendant. Les métriques suivantes sont analysées :
- **Précision, Recall, F1-score** : Évaluation de la qualité des prédictions.
- **Score AUC** : Indicateur de la capacité du modèle à distinguer les classes positives et négatives.

---

## 🚀 **6. Déploiement**

### 📦 1. Sauvegarde du modèle
Le modèle final est sauvegardé sous forme d’un fichier pour pouvoir être réutilisé sans nécessiter un nouvel entraînement.

### 🌍 2. Création d'une API avec Flask
Une API est développée pour permettre à d'autres applications d'envoyer des données et de recevoir une prédiction en retour. L’API prend en entrée les caractéristiques d’un patient et retourne la probabilité qu’il soit atteint d’une maladie cardiovasculaire.

### ✅ 3. Tests et documentation
Avant le déploiement, des tests sont réalisés pour valider le bon fonctionnement de l'API. Une documentation détaillant l'utilisation de l'API est également rédigée pour faciliter son intégration dans un environnement réel.

---

## 🎯 **7. Impact et Applications**
- **Aide au diagnostic médical** : Prédire le risque cardiovasculaire d’un patient en fonction de ses caractéristiques médicales et habitudes de vie.
- **Prévention des MCV** : Identifier les individus à haut risque pour une prise en charge précoce et une amélioration des comportements à risque.
- **Optimisation des politiques de santé** : Utiliser les prédictions du modèle pour mieux orienter les campagnes de prévention et de sensibilisation.

---

## 🔥 **8. Résumé**
1. **Analyse descriptive** : Exploration et visualisation des variables pour comprendre les tendances et relations.
2. **Préparation des données** : Nettoyage, gestion des valeurs aberrantes, normalisation et encodage des variables.
3. **Modélisation** : Sélection du meilleur modèle et optimisation des hyperparamètres.
4. **Déploiement** : Mise en place d’une API pour permettre l’exploitation du modèle dans un environnement réel.

🚀 **Un projet complet, de l'analyse des données jusqu'au déploiement d’un outil d’aide à la décision !**
