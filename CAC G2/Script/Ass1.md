<img src="WhatsApp Image 2025-10-29 at 11.36.26.pdf" style="height:464px;margin-right:432px"/>
## Hassi Asmae
## 24010417

#  Base de données : Adult (Census Income)

## Présentation générale
La base de données **Adult**, aussi appelée **Census Income Dataset**, provient du **recensement américain de 1994**.  
Elle a été collectée par le **U.S. Census Bureau** et préparée par **Ronny Kohavi** et **Barry Becker** (Stanford University).  
Elle est disponible sur le site du **[UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/adult)**.

---

##  Objectif du jeu de données
L’objectif principal est de **prédire si une personne gagne plus de 50 000 $ par an** à partir de ses caractéristiques démographiques et professionnelles.  

Il s’agit d’un **problème de classification supervisée binaire** :

- **Classe 1 :** Revenu > 50K USD  
- **Classe 0 :** Revenu ≤ 50K USD  

Cette base est fréquemment utilisée pour **tester et comparer la performance** d’algorithmes de machine learning tels que :  
- la **régression logistique**,  
- les **arbres de décision**,  
- les **forêts aléatoires**,  
- ou encore les **réseaux de neurones**.

---

##  Contenu des données
La base contient environ **48 842 observations** et **15 variables**.  
Chaque ligne représente un **individu** et ses **caractéristiques socio-économiques**.

| Nom de la variable |  Traduction / Signification |  Type |
|------------------------|-------------------------------|--------|
| `age` | Âge de la personne | Numérique |
| `workclass` | Type d’emploi (secteur privé, public, indépendant, etc.) | Catégorielle |
| `fnlwgt` | Poids statistique (nombre de personnes représentées par l’individu) | Numérique |
| `education` | Niveau d’éducation | Catégorielle |
| `education-num` | Niveau d’éducation (valeur numérique) | Numérique |
| `marital-status` | Situation matrimoniale | Catégorielle |
| `occupation` | Profession exercée | Catégorielle |
| `relationship` | Rôle dans le foyer (chef, épouse, enfant, etc.) | Catégorielle |
| `race` | Origine ethnique | Catégorielle |
| `sex` | Sexe | Catégorielle |
| `capital-gain` | Gains en capital (hors salaire) | Numérique |
| `capital-loss` | Pertes en capital | Numérique |
| `hours-per-week` | Heures de travail hebdomadaires | Numérique |
| `native-country` | Pays d’origine | Catégorielle |
| `income` | Revenu cible (>50K ou <=50K) | Catégorielle (binaire) |

---

##  Intérêt de l’analyse
L’étude de cette base permet de :

-  **Analyser les facteurs socio-économiques** qui influencent le revenu des individus ;  
-  **Étudier les inégalités de revenus** selon le sexe, la profession ou le niveau d’éducation ;  
- **Construire et tester des modèles prédictifs** pour la classification binaire ;  
   **Comprendre les interactions entre variables démographiques et professionnelles**.

---

##  Interprétation des visualisations (exemples)
### Distribution du revenu (`income`)
La majorité des individus se trouve dans la catégorie **« <=50K »**. Le jeu est déséquilibré et il faudra en tenir compte lors de la modélisation (stratification, sur-échantillonnage, ou métriques adaptées).

### Age vs Income
Les personnes avec un revenu >50K sont plus fréquentes dans des tranches d’âge moyennes à élevées (en général 35-60 ans), ce qui suggère un lien entre expérience/ancienneté et niveau de revenu.

---

## Remarques pratiques
- Les valeurs `'?'` dans certaines colonnes indiquent des **valeurs manquantes** ; il est conseillé de les remplacer ou d’utiliser des techniques d’imputation.  
- `fnlwgt` est un **poids d’échantillonnage** ; selon l’objectif, il peut être utilisé ou ignoré pour la modélisation.  
- `capital-gain` et `capital-loss` sont très **sparse** (beaucoup de zéros) et peuvent nécessiter une transformation (log + binarisation).

---

##  Licence et source
Données : UCI Machine Learning Repository — *Adult Data Set*  
Licence : données publiques (vérifier la page UCI pour les conditions d’utilisation exactes).
#  Interprétation des visualisations

##  1. Distribution du revenu (`income`)
![Distribution du revenu](<img width="558" height="393" alt="dis" src="https://github.com/user-attachments/assets/b9ef91f9-d04e-4945-be4a-13de855c6b47" />
.png)

Le premier graphique montre la répartition des individus selon leur niveau de revenu.  

On observe que la majorité des personnes se trouvent dans la catégorie **“≤ 50K”**, c’est-à-dire qu’elles gagnent moins de 50 000 dollars par an.  
Le groupe des individus **“> 50K”** est nettement moins représenté.  

 **Conclusion :**  
La base de données est **déséquilibrée** — les revenus faibles sont beaucoup plus fréquents que les revenus élevés.  

 **Interprétation logique :**  
Cette différence reflète la réalité socio-économique : la proportion de personnes à hauts revenus est naturellement plus faible dans une population générale.  
Ce déséquilibre devra être pris en compte lors de la modélisation pour éviter que le modèle ne privilégie la classe majoritaire (“≤50K”).

---

##  2. Distribution de l’âge selon le revenu (`age` par `income`)
![Distribution de l’âge selon le revenu](<img width="859" height="547" alt="distribution" src="https://github.com/user-attachments/assets/640e260e-73e9-4115-b86d-5b9282c6a755" />
.png)

Ce graphique représente la répartition des âges en fonction du niveau de revenu.  

On constate que :
- la plupart des individus gagnant **≤50K** se situent dans la tranche **20 à 40 ans** ;
- les individus ayant un revenu **>50K** sont plus nombreux dans la tranche **35 à 60 ans** ;
- la densité de revenu élevé diminue légèrement **après 60 ans**.

 **Conclusion :**  
Le revenu semble **augmenter avec l’expérience et l’ancienneté professionnelle.**

 **Interprétation logique :**
Les personnes plus âgées ont généralement :
- une **éducation plus complète**,  
- une **stabilité de carrière**,  
- et souvent des **postes à responsabilité**.  

Cela explique pourquoi elles appartiennent plus souvent à la catégorie des revenus supérieurs.
## 🔹 3. Distribution des heures de travail hebdomadaires selon le revenu (`hours-per-week` par `income`)

![Distribution des heures de travail](<img width="868" height="547" alt="image" src="https://github.com/user-attachments/assets/db99ad85-6962-4a55-af86-ac7b3f2cbc88" />


.png)

On remarque que les individus gagnant **>50K** ont tendance à travailler **davantage d’heures par semaine** que ceux gagnant ≤50K.  
La majorité des revenus faibles se concentre autour de **40 heures hebdomadaires**, alors que les hauts revenus s’étendent souvent jusqu’à **50 à 60 heures par semaine**.

 **Interprétation:**  
Les personnes à revenus élevés :
- occupent souvent des **postes à responsabilités**,  
- travaillent **plus longtemps** ou dans des emplois exigeants,  
- et sont parfois **indépendantes ou cadres supérieurs**.

Ainsi, la **quantité d’heures travaillées** semble être un **facteur corrélé positivement** au revenu annuel.

---

##  4. Distribution du niveau d’éducation selon le revenu (`education` par `income`)

![Distribution du niveau d’éducation](<img width="1189" height="690" alt="dist" src="https://github.com/user-attachments/assets/dc2244c9-10e9-481a-b3f0-ef642634dd51" />
.png)

On constate que :
- Les individus avec un **niveau d’éducation faible** (ex. : “HS-grad”, “Some-college”) se retrouvent majoritairement dans la catégorie **≤50K**.  
- Les individus ayant un **niveau d’éducation supérieur** (ex. : “Bachelors”, “Masters”, “Doctorate”) sont surreprésentés dans la catégorie **>50K**.

 **Interprétation:**  
Le **niveau d’éducation** influence fortement le **niveau de revenu** :
- plus le niveau d’études est **élevé**, plus la probabilité d’avoir un **revenu supérieur à 50K** augmente.  
Cela traduit une **corrélation claire entre formation et revenus**.

---

##  3. Conclusion générale

Ces premières analyses confirment que :
- le **revenu dépend fortement de l’âge**, et sans doute aussi d’autres facteurs comme **l’éducation** ou **la profession** ;  
- la majorité des individus gagnent **moins de 50K**, ce qui devra être pris en compte pour **équilibrer les classes** dans la modélisation.  

 **Résumé :**  
Ces visualisations constituent une **étape essentielle** de la compréhension des données avant toute modélisation prédictive.  
Elles permettent de dégager des **tendances socio-économiques claires** et de **préparer le terrain pour une analyse plus approfondie**.


---


