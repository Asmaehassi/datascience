<img src="WhatsApp Image 2025-10-29 at 11.36.26.pdf" style="height:464px;margin-right:432px"/>
## Hassi Asmae
## 24010417

 la base de données Adult (Census Income)
 1. Présentation générale

La base de données Adult, aussi appelée Census Income Dataset, provient du recensement américain de 1994.
Elle a été collectée par le U.S. Census Bureau et préparée par Ronny Kohavi et Barry Becker (Stanford University).
Elle est disponible sur le site du UCI Machine Learning Repository.

 2. Objectif du jeu de données

L’objectif principal est de prédire si une personne gagne plus de 50 000 $ par an à partir de ses caractéristiques démographiques et professionnelles.
Il s’agit donc d’un problème de classification supervisée binaire :

Classe 1 : Revenu > 50K USD

Classe 0 : Revenu ≤ 50K USD

Cette base est souvent utilisée pour tester et comparer la performance d’algorithmes de machine learning (régression logistique, arbres de décision, forêts aléatoires, etc.).

3. Contenu des données

La base contient environ 48 842 observations et 15 variables.
Chaque ligne représente un individu et ses caractéristiques.

Nom de la variable	Traduction / Signification	Type
age	Âge de la personne	Numérique
workclass	Type d’emploi (secteur privé, public, indépendant, etc.)	Catégorielle
fnlwgt	Poids statistique (nombre de personnes représentées par l’individu)	Numérique
education	Niveau d’éducation	Catégorielle
education-num	Niveau d’éducation (valeur numérique)	Numérique
marital-status	Situation matrimoniale	Catégorielle
occupation	Profession exercée	Catégorielle
relationship	Rôle dans le foyer (chef, épouse, enfant, etc.)	Catégorielle
race	Origine ethnique	Catégorielle
sex	Sexe	Catégorielle
capital-gain	Gains en capital (hors salaire)	Numérique
capital-loss	Pertes en capital	Numérique
hours-per-week	Heures de travail hebdomadaires	Numérique
native-country	Pays d’origine	Catégorielle
income	Revenu cible (>50K ou <=50K)	Catégorielle (binaire)
 4. Intérêt de l’analyse

Cette base permet :

D’étudier les facteurs socio-économiques influençant le revenu ;

D’analyser les inégalités de revenus selon le sexe, la profession ou l’éducation ;

De tester des modèles de prédiction de manière pratique et réaliste.

 5. Exemple d’interprétation

Des visualisations simples permettent de mieux comprendre la distribution des données :

La majorité des individus gagnent moins de 50 000 $ ;

Les personnes ayant un niveau d’éducation élevé et travaillant plus d’heures par semaine ont plus de chances de dépasser ce seuil de revenu ;

Il existe une différence notable entre hommes et femmes en termes de revenus.

 6. Conclusion

La base Adult constitue un jeu de données de référence pour les projets de classification.
Elle combine variables socio-démographiques réelles et richesse statistique, ce qui la rend idéale pour :

la visualisation de données,

la modélisation prédictive,

et la découverte d’insights socio-économiques.

Interprétation des visualisations

1. Distribution du revenu (income)

Le premier graphique montre la répartition des individus selon leur niveau de revenu.

On observe que la majorité des personnes se trouvent dans la catégorie “<=50K”, c’est-à-dire qu’elles gagnent moins de 50 000 dollars par an.

Le groupe des individus “>50K” est nettement moins représenté.

Cela indique que la base de données est déséquilibrée : les revenus faibles sont beaucoup plus fréquents que les revenus élevés.

 Interprétation :
Cette différence reflète la réalité socio-économique : la proportion de personnes à hauts revenus est naturellement plus faible dans une population générale.
Ce déséquilibre devra être pris en compte lors de la modélisation, pour éviter que le modèle ne privilégie la classe majoritaire (“<=50K”).

 2. Distribution de l’âge selon le revenu (age par income)

Le second graphique représente la répartition des âges en fonction du niveau de revenu.

On constate que la plupart des individus gagnant ≤50K se situent dans la tranche jeune à moyenne (20 à 40 ans).

Les individus ayant un revenu >50K sont plus nombreux dans les tranches d’âge supérieures (35 à 60 ans).

La densité de revenu élevé augmente donc avec l’âge, puis tend à diminuer légèrement après 60 ans.

Interprétation :
Le revenu semble croître avec l’expérience et l’ancienneté professionnelle.
Les personnes plus âgées ont généralement :

une éducation plus complète,

une stabilité de carrière,

et souvent des postes à responsabilité.

Cela explique pourquoi elles ont davantage de chances d’appartenir à la catégorie des revenus supérieurs.

3. Conclusion générale sur ces visualisations

Ces premières analyses confirment que :

le revenu dépend fortement de l’âge et sans doute aussi d’autres facteurs socio-économiques (comme l’éducation ou la profession) ;

la majorité de la population gagne moins de 50K, ce qui doit être pris en compte dans la modélisation pour équilibrer les classes.

Ces visualisations constituent donc une première étape essentielle de la compréhension des données avant toute modélisation prédictive.
