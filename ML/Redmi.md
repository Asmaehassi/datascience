#   Classification de la Qualité du Vin (k-NN)

Ce projet applique une chaîne complète d’apprentissage supervisé pour prédire si un vin est de **bonne** ou **mauvaise** qualité à partir de ses caractéristiques physico-chimiques.

---

#  Objectif
- Prédire la **qualité du vin** (binaire : 0 = mauvais, 1 = bon)
- Utiliser l’algorithme **k-Nearest Neighbors (k-NN)**
- Comparer les résultats **avec** et **sans normalisation**

---

#  Analyse des données

Le dataset contient :
- **4898 échantillons**
- **11 variables** physico-chimiques (acidité, sucre, pH, sulfates…)
- Une note de qualité (3 à 9), transformée en :
  - 0 = qualité ≤ 5  
  - 1 = qualité ≥ 6

### Points importants :
- Certaines variables sont très corrélées (ex : sucre résiduel & densité)
- Les échelles sont différentes → **normalisation fortement recommandée**

---

#  Modélisation

##  Étapes suivies
1. Découpage Stratifié Train / Validation / Test  
2. Entraînement du k-NN avec plusieurs valeurs de k  
3. Analyse des erreurs  
4. Choix du meilleur k  
5. Normalisation des données et comparaison  
6. Matrices de confusion

Compris Esma ! ✔
Je vais te donner **un README GitHub complet**, clair, professionnel, prêt à coller dans ton dépôt.
Il contient :

Objectif du TP
Chargement des données + code commenté
Analyse statistique (boxplot + heatmap)
Classification k-NN complète
Interprétation + conclusions
 Structure du projet GitHub
 Emplacement exact pour les figures

**Tu n’auras qu’à copier-coller dans ton GitHub.**

---


````markdown
#  Classification de la qualité du vin – TP Machine Learning

## Objectif
Apprendre un modèle prédictif permettant de classifier la qualité du vin blanc 
à partir de caractéristiques physico-chimiques.  

Le dataset provient de l’UCI Machine Learning Repository :  
http://archive.ics.uci.edu/ml/datasets/Wine+Quality  

Le but est de :
- charger les données,  
- analyser les variables,  
- construire un classifieur k-NN,  
- choisir le meilleur k,  
- comparer les résultats avant/après normalisation.

---

#  1. Préparation de l’environnement

```bash
source /opt/venv/iti-data/bin/activate
jupyter-notebook &
spyder &
````

Pour obtenir l’aide d’une fonction :

```python
from sklearn.neighbors import KNeighborsClassifier
?KNeighborsClassifier
```

---

# 2. Chargement du dataset

```python
import pandas as pd
import numpy as np

link = "http://archive.ics.uci.edu/ml/machine-learning-databases/winequality/winequality-white.csv"
df = pd.read_csv(link, header="infer", delimiter=";")

df.info()
df.head()
```

###  Interprétation

* Le dataset contient **4898 échantillons**.
* Chaque vin possède **11 variables physico-chimiques**.
* La variable `quality` représente une note de 0 à 10.

---

#  3. Construction de X et Y

```python
X = df.drop("quality", axis=1)
Y = df["quality"]

print(Y.value_counts())
```

###  Commentaires

* X contient les variables d'entrée (features).
* Y contient la qualité brute (0–10).
* La distribution est déséquilibrée : les notes 5, 6, 7 dominent.

---

#  4. Transformation en classification binaire

```python
Y = [0 if val <= 5 else 1 for val in Y]
```

### Commentaire

* 0 = vin de qualité faible ou moyenne
* 1 = vin de bonne qualité
* Cela simplifie le problème en **classification binaire**.

---

# 5. Analyse statistique

## 5.1 Boxplot des variables

<img width="552" height="529" alt="image" src="https://github.com/user-attachments/assets/921106b9-3380-41bf-a8e4-e81a2442ea1c" />


**Interprétation :**
- Forte présence d’outliers dans plusieurs variables.  
- Des échelles très différentes entre les variables (ex : residual sugar vs chlorides).  
- Certaines variables présentent une forte asymétrie.  
- Ces observations montrent qu’il est nécessaire d’appliquer une **normalisation** avant d’entraîner un modèle basé sur les distances comme k-NN.

---


```python
plt.figure()
ax = plt.gca()
sns.boxplot(data=X, orient="v", palette="Set1", width=1.5, notch=True)
ax.set_xticklabels(ax.get_xticklabels(), rotation=90)
```




---

## 5.2 Matrice de corrélation (Heatmap)

<img width="643" height="535" alt="image" src="https://github.com/user-attachments/assets/6aba12b5-386f-414f-a595-98fb887e05ea" />



**Interprétation :**
- **Corrélation élevée** entre :
  - *density* et *residual sugar*  
  - *free sulfur dioxide* et *total sulfur dioxide*  
- Corrélation négative entre *pH* et *fixed acidity*.  
- Plusieurs variables ont des corrélations faibles → elles apportent des informations indépendantes.

**Conclusion :**

```python
corr = X.corr()
sns.heatmap(corr)
```

###  Interprétation

* *density* ↔ *residual sugar* = corrélation forte positive
* *free sulfur dioxide* ↔ *total sulfur dioxide* = très lié
* *pH* ↔ *fixed acidity* = corrélation négative
* Certaines variables sont indépendantes → information utile pour le modèle



---

#  6. Classification

## 6.1 Split du dataset

```python
from sklearn.model_selection import train_test_split

Xa, Xt, Ya, Yt = train_test_split(X, Y, shuffle=True, test_size=1/3, stratify=Y)
Xa, Xv, Ya, Yv = train_test_split(Xa, Ya, shuffle=True, test_size=0.5, stratify=Ya)
```



---

## 6.2 Premier modèle k-NN avec k=3

```python
k = 3
clf = KNeighborsClassifier(n_neighbors=k)
clf.fit(Xa, Ya)

Ypred_v = clf.predict(Xv)

from sklearn.metrics import accuracy_score
error_v = 1 - accuracy_score(Yv, Ypred_v)
```

###  Interprétation

* k=3 → très sensible au bruit
* Le modèle peut sur-apprendre → mauvaise généralisation sur validation

---

## 6.3 Choix du meilleur k

```python
k_vector = np.arange(1, 37, 2)
error_train = np.empty(k_vector.shape)
error_val = np.empty(k_vector.shape)

for ind, k in enumerate(k_vector):
    clf = KNeighborsClassifier(n_neighbors=k)
    clf.fit(Xa, Ya)

    Ypred_train = clf.predict(Xa)
    error_train[ind] = 1 - accuracy_score(Ya, Ypred_train)

    Ypred_val = clf.predict(Xv)
    error_val[ind] = 1 - accuracy_score(Yv, Ypred_val)
```

###  Interprétation

* Petit k → surapprentissage (erreur train très faible, erreur val élevée)
* Grand k → sous-apprentissage
* Le meilleur k minimise **l’erreur validation**.

```python
err_min, ind_opt = error_val.min(), error_val.argmin()
k_star = k_vector[ind_opt]
```

---

## 6.4 Evaluation finale sur le test set

```python
clf = KNeighborsClassifier(n_neighbors=k_star)
clf.fit(Xa, Ya)
Ypred_test = clf.predict(Xt)

error_test = 1 - accuracy_score(Yt, Ypred_test)
```

###  Interprétation

* L’erreur test reflète la performance **réelle** du modèle.
* Elle doit être proche de l’erreur validation → bon modèle.

---

# 7. Normalisation des données

```python
from sklearn.preprocessing import StandardScaler

sc = StandardScaler(with_mean=True, with_std=True)
sc = sc.fit(Xa)

Xa_n = sc.transform(Xa)
Xv_n = sc.transform(Xv)
```

###  Commentaires

* On calcule moyenne/variance **uniquement sur Xa** → bonne pratique
* On applique ensuite cette transformation sur validation et test
* La normalisation améliore fortement k-NN car basé sur la **distance**

---


---


- Les corrélations nous apprennent quelles variables influencent potentiellement la qualité du vin.  
- Elles confirment l’intérêt d’une normalisation et d’un modèle robuste aux variations d’échelle.


---

#  Résultats

| Données            | k* optimal | Erreur validation | Erreur test |
|-------------------|------------|------------------|-------------|
| Brutes            | 17         | ~0.182           | ~0.182      |
| Normalisées       | 9          | ~0.148           | ~0.151      |

➡ La normalisation améliore la précision de **3 à 4 points**.

---

#  Conclusion
- Le k-NN fonctionne beaucoup mieux avec des données **normalisées**.
- Le meilleur modèle obtenu : **k = 9** avec normalisation.
- La pipeline montre une méthodologie complète : EDA, split, optimisation, évaluation.

---






