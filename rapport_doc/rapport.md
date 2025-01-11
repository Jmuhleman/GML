# Rapport Final : Projet Predictus Olympiae

### Julien Mühlemann, Cristhian Ronquillo, Dr. Ing. Julien Billeter

## Table des Matières
1. [Introduction](#introduction)  
2. [Présentation du Projet](#présentation-du-projet)  
   2.1 [Contexte](#contexte)  
   2.2 [Problématique](#problématique)  
   2.3 [Objectifs](#objectifs)  
3. [Technologies et Données](#technologies-et-données)  
   3.1 [Technologies Utilisées](#technologies-utilisées)  
   3.2 [Sources de Données](#sources-de-données)  
4. [Méthodologie](#méthodologie)  
   4.1 [Planification et Organisation](#planification-et-organisation)  
   4.2 [Approches Supervisée et Non Supervisée](#approches-supervisée-et-non-supervisée)  
5. [Implémentation](#implémentation)  
   5.1 [Préparation des Données](#préparation-des-données)  
   5.2 [Analyse exploratoire des Données]()  
   5.3 [Méthodes Non Supervisées](#méthodes-non-supervisées)
   5.4 [Méthodes Supervisées](#méthodes-supervisées) 
6. [Résultats et Analyse](#résultats-et-analyse)  
   6.1 [Performances des Modèles](#performances-des-modèles)  
   6.2 [Insights Clés](#insights-clés)  
7. [Plan d’Assurance Qualité](#plan-dassurance-qualité)  
   7.1 [Contrôle des Données](#contrôle-des-données)  
   7.2 [Validation et Revue de Code](#validation-et-revue-de-code)  
8. [Discussion et Limites](#discussion-et-limites)  
   8.1 [Forces et Faiblesses](#forces-et-faiblesses)  
   8.2 [Améliorations Futures](#améliorations-futures)  
9. [Conclusion](#conclusion)
10. [Références](#références)
11. [Annexes](#annexes)  
    10.1 [Journal de Travail](#journal-de-travail)  
    10.2 [Code Source et Documentation](#code-source-et-documentation)  

---

## 1. Introduction

Les Jeux olympiques, véritable vitrine des performances sportives mondiales, représentent bien plus qu’un simple événement sportif. Ils incarnent l’excellence, le dépassement de soi, et sont souvent perçus comme un reflet des capacités économiques, culturelles et organisationnelles des nations participantes.

Le projet **Predictus Olympiae** s’inscrit dans cette dynamique, visant à modéliser et prédire les performances olympiques des pays en fonction de multiples variables, telles que les données socio-économiques, démographiques et historiques. L’objectif ultime est de fournir un outil analytique robuste pour mieux comprendre les déterminants du succès sportif et éclairer les stratégies nationales.

---

## 2. Présentation du Projet

### 2.1 Contexte
Depuis leur résurrection moderne en 1896, les Jeux olympiques sont devenus un symbole global de l’unité et de la compétition entre nations. Chaque médaille remportée témoigne non seulement des efforts individuels, mais aussi du soutien institutionnel et des investissements nationaux dans le sport.

Dans ce contexte, le projet **Predictus Olympiae** ambitionne d’identifier les facteurs clés permettant de prédire les performances olympiques. En s’appuyant sur des données variées, il explore les liens entre des variables telles que le PIB, la population, les dépenses en infrastructures sportives, et les résultats sportifs passés.

### 2.2 Problématique
La prédiction des performances olympiques constitue un défi complexe pour plusieurs raisons :  
- **Hétérogénéité des données** : Les variables influençant les performances sportives proviennent de domaines variés (économie, politique, climat).  
- **Complexité des interactions** : Les relations entre ces variables sont rarement linéaires et peuvent inclure des effets multiplicateurs ou contextuels.  
- **Données historiques incomplètes** : Certaines variables, telles que le financement sportif ou les données démographiques spécifiques, ne sont pas toujours disponibles ou homogènes.  
Le projet doit donc relever ces défis pour construire des modèles fiables et interprétables.

### 2.3 Objectifs
Le projet s’articule autour des objectifs suivants :  
- **Must Have** :  
  - Développer un modèle prédictif performant basé sur l’apprentissage supervisé pour estimer les performances des pays aux Jeux olympiques.  
  - Fournir des prédictions exploitables pour un large éventail de disciplines sportives.  
- **Nice to Have** :  
  - Produire une analyse détaillée par discipline sportive afin d’identifier les forces et faiblesses des pays.  
  - Explorer des techniques avancées d’optimisation des modèles, telles que le fine-tuning des hyperparamètres ou l’intégration d’approches de deep learning.  
  

---

## 3. Technologies et Données

### 3.1 Sources de Données
Le projet **Predictus Olympiae** repose sur une collecte et une exploitation rigoureuse de données provenant de diverses sources fiables. Les principales catégories de données utilisées incluent :  
- **Données historiques des résulats olympiques** : Informations sur les performances des nations aux Jeux olympiques passés, via Kaggle [1]. Nous avons transformé les données brutes en un format tel qu'il représente le nombre d'athlètes par nation présent dans les 10 premiers pour chaque discipline.

- **Données socio-économiques et démographiques** : Informations issues notamment des ensembles de données de Gapminder, ces données couvrent des indicateurs tels que :  
  - **Mortalité infantile** : Mesure du taux de mortalité des enfants de moins de cinq ans, reflétant les conditions de santé et de développement d’une nation.  
  - **Fertilité** : Nombre moyen d’enfants par femme, indicateur clé des dynamiques démographiques.  
  - **PIB par habitant** : Représentant la richesse économique d’un pays, il est essentiel pour comprendre les ressources disponibles pour le développement sportif.  
  - **Espérance de vie** : Indicateur de la qualité de vie globale et des infrastructures de santé.  
  - **Population totale** : Facteur influençant la taille du vivier de talents sportifs disponibles dans chaque pays.  

- **Données climatiques** : xxx

Ces données ont été extraites, nettoyées et combinées pour former une base solide permettant l’entraînement et la validation des modèles prédictifs développés dans ce projet. La richesse et la variété de ces sources offrent une vue d’ensemble des déterminants possibles des performances olympiques, tout en fournissant une granularité suffisante pour des analyses approfondies.  

Nous avons choisi de travailler sur les disciplines suivantes :
```python
sports_summer_before_1988 = [
    'Shooting', 'Diving', 'Canoe Sprint', 'Cycling Road', 'Football', 'Boxing', 'Basketball',
    'Cycling Track', 'Fencing', 'Water Polo', 'Wrestling', 'Artistic Gymnastics', 'Weightlifting',
    'Modern Pentathlon', 'Hockey', 'Athletics', 'Swimming', 'Sailing', 'Rowing'
]
sports_summer_after_1988 = [
    'Shooting', 'Diving', 'Canoe Sprint', 'Cycling Road', 'Football', 'Boxing', 'Basketball',
    'Cycling Track', 'Fencing', 'Table Tennis', 'Badminton', 'Water Polo', 'Wrestling',
    'Artistic Gymnastics', 'Canoe Slalom', 'Rhythmic Gymnastics', 'Weightlifting', 'Modern Pentathlon',
    'Hockey', 'Volleyball', 'Artistic Swimming', 'Athletics', 'Swimming', 'Sailing', 'Rowing',
    'Tennis', 'Equestrian', 'Archery', 'Handball', 'Judo'
]
```
En effet, pour les disciplines restantes nous n'avons pas jugé que l'historiques des performance était suffisant.

## 4. Méthodologie
### 4.1 Planification et Organisation
distribution des tâches, répartition des rôles, gestion des délais, communication interne, etc.

### 4.2 Approches Supervisée et Non Supervisée



---
## 5. Implémentation

### 5.1 Préparation des Données
La préparation des données a constitué une étape cruciale du projet, notamment en raison des divergences observées dans les noms des pays selon les différentes sources utilisées. Ces conflits provenaient des différences linguistiques (anglais, français), des variations dans la nomenclature des pays (utilisation de noms officiels ou abrégés), et des évolutions géopolitiques au fil du temps (changements de noms de pays, disparition ou création de nouvelles entités étatiques).  

Les données issues de **Gapminder** et de **Kaggle** ont nécessité une harmonisation manuelle, ce qui a représenté un effort conséquent. Par exemple :  
- Certains pays étaient désignés par des noms différents dans les deux bases, tels que "Côte d'Ivoire" (français) et "Ivory Coast" (anglais).  
- D'autres pays étaient répertoriés sous des appellations historiques ou obsolètes, comme "URSS" pour des données antérieures à sa dissolution, tandis que les données récentes utilisaient les noms des pays indépendants issus de son éclatement.  
- Dans certains cas, des entités telles que "République tchèque" et "Tchécoslovaquie" coexistaient dans les jeux de données, nécessitant un regroupement ou une distinction en fonction de la période.  

Cette étape a nécessité plusieurs jours de travail pour ajuster manuellement la liste des pays, garantir leur uniformité, et aligner les données sur une nomenclature commune. Une attention particulière a été portée aux subtilités historiques et linguistiques afin de minimiser les erreurs d'interprétation et d'assurer la fiabilité des analyses.  

### 5.2 Analyse Exploratoire des Données 
 
La relation entre le attributs, les pays et les performances aux JO sont difficiles à observer visuellement. Pour cette raison nous avons moyenné pour chacun des pays les attributs et le score. 

| Pays               | Population   | Fertilité    | sig_fertility | child       | sig_child   | PIB par habitant | sig_gdp     | Temperature   | Précipitations | Saisonalité  | Aridité     | score    | sig_score    |
|--------------------|-------------|--------------|---------------|-------------|-------------|------------------|-------------|---------------|----------------|--------------|-------------|----------|-------------|
| USA                | 0.227 | 0.147 | x   | 0.02728728  | 0.010453432 | 0.317685243      | 0.035464536 | 0.481818182   | 0.463636364    | 0.4          | 0.395454545 | 213.125  | 13.60081405 |
| Germany            | 0.063 | 0.07 | x   | 0.009224227 | 0.003280202 | 0.274660395      | 0.031615295 | 0.333333333   | 0.333333333    | 0.3          | 0.333333333 | 152.375  | 31.01583697 |
| China              | 1 | 0.10 | x | 0.105743496 | 0.040484548 | 0.039441399      | 0.024236932 | 0.43125       | 0.45625        | 0.36875      | 0.35        | 133.5    | 26.14246682 |
| Australia          | 0.016 | 0.13 | x | 0.012043604 | 0.003191327 | 0.252701518      | 0.020309906 | 0.6           | 0.583333333    | 0.475        | 0.466666667 | 115.25   | 19.47709277 |
| Russia             | 0.112 | 0.08 | x | 0.053476517 | 0.008833567 | 0.120114151      | 0.016545476 | 0.366666667   | 0.36           | 0.326666667  | 0.34        | 111.75   | 72.10458674 |
| Great Britain      | 0.0471 | 0.12 | x | 0.014664793 | 0.005237619 | 0.239166775      | 0.025311459 | 0.45          | 0.55           | 0.45         | 0.45        | 110.375  | 28.00988346 |
| France             | 0.0471 | 0.140107992  | 0.026314226   | 0.010551804 | 0.005078353 | 0.247743133      | 0.036498175 | 0.625         | 0.675          | 0.575        | 0.375       | 106.5    | 5.806400409 |
| Italy              | 0.045 | 0.056067033  | 0.018449868   | 0.00895299  | 0.001312416 | 0.251034083      | 0.049381484 | 0.4625        | 0.5            | 0.4125       | 0.4         | 90.75    | 12.08008988 |
| Japan              | 0.097 | 0.062875866  | 0.014141373   | 0.003712824 | 0.001795104 | 0.233179106      | 0.046170304 | 0.516666667   | 0.533333333    | 0.466666667  | 0.4         | 84.875   | 18.58907129 |
| Canada             | 0.025 | 0.097461137  | 0.012213047   | 0.016421301 | 0.008382053 | 0.259074901      | 0.030000094 | 0.358333333   | 0.358333333    | 0.325        | 0.35        | 71.375   | 10.41890452 |
| South Korea        | 0.0367 | 0.049571993  | 0.033977696   | 0.014276859 | 0.004915931 | 0.171994483      | 0.023403039 | 0.45          | 0.466666667    | 0.416666667  | 0.35        | 68       | 6.187545094 |
| Poland             | 0.029 | 0.074736976  | 0.029482876   | 0.024921788 | 0.005387387 | 0.118569014      | 0.024364297 | 0.466666667   | 0.433333333    | 0.4          | 0.433333333 | 64.625   | 9.318759881 |
| Spain              | 0.0334 | 0.050388407  | 0.018245106   | 0.008318469 | 0.001295534 | 0.20878213       | 0.025508513 | 0.5           | 0.566666667    | 0.433333333  | 0.5         | 60.875   | 9.218575967 |
| Hungary            | 0.0077 | 0.077290196  | 0.036251145   | 0.024722662 | 0.003922795 | 0.133428535      | 0.011814265 | 0.5           | 0.5            | 0.45         | 0.45        | 57.25    | 11.79285498 |
| Ukraine            | 0.037 | 0.060962825  | 0.024075875   | 0.056593534 | 0.005634556 | 0.064067974      | 0.018340372 | 0.483333333   | 0.466666667    | 0.416666667  | 0.45        | 56.875   | 25.36835768 |
| Netherlands        | 0.0125 | 0.109236967  | 0.022825091   | 0.01150047  | 0.003631768 | 0.289872819      | 0.027381287 | 0.5           | 0.6            | 0.5          | 0.5         | 56.375   | 13.710658   |
| Cuba               | 0.0085 | 0.092510991  | 0.016154994   | 0.022594292 | 0.003035092 | 0.033293222      | 0.006235419 | 0.8           | 0.833333333    | 0.7          | 0.233333333 | 53.375   | 13.59556125 |
| Brazil             | 0.140 | 0.164777066  | 0.044931881   | 0.12364991  | 0.025332691 | 0.075583273      | 0.007427943 | 0.644444444   | 0.744444444    | 0.6          | 0.311111111 | 42       | 20.52872552 |
| Sweden             | 0.0071 | 0.127464587  | 0.029377761   | 0.003191197 | 0.002863273 | 0.263575656      | 0.017553042 | 0.375         | 0.35           | 0.325        | 0.35        | 40.125   | 9.372261505 |
| Belarus            | 0.0074 | 0.0774875    | 0.033962225   | 0.025858457 | 0.010981238 | 0.074173279      | 0.017102739 | 0.5           | 0.5            | 0.45         | 0.45        | 39.5     | 17.96822592 |
| Romania            | 0.016 | 0.084490966  | 0.042490226   | 0.066148806 | 0.014395207 | 0.103245512      | 0.023607283 | 0.46          | 0.46           | 0.4          | 0.48        | 37.5     | 16.34450541 |
| New Zealand        | 0.0032 | 0.155028409  | 0.012263782   | 0.021386144 | 0.008037205 | 0.215960769      | 0.017803561 | 0.333333333   | 0.4            | 0.333333333  | 0.333333333 | 32.5     | 8.451542547 |
| Denmark            | 0.0042 | 0.125390764  | 0.021610259   | 0.010910354 | 0.005427115 | 0.298401012      | 0.037642199 | 0.5           | 0.6            | 0.5          | 0.5         | 30.875   | 5.303300859 |
| Kazakhstan         | 0.0130 | 0.243607005  | 0.101765653   | 0.124913259 | 0.044476965 | 0.098191087      | 0.021214289 | 0.43          | 0.37           | 0.33         | 0.43        | 27.5     | 12.27075501 |
| Bulgaria           | 0.0059 | 0.076610831  | 0.034730001   | 0.049981286 | 0.006319513 | 0.091066127      | 0.013625389 | 0.56          | 0.62           | 0.5          | 0.46        | 27.25    | 13.64603553 |
| Czech Republic     | 0.0079 | 0.080122095  | 0.054042326   | 0.009556825 | 0.00425697  | 0.175510753      | 0.009384674 | 0.5           | 0.5            | 0.45         | 0.45        | 27.25    | 11.47357212 |
| Greece             | 0.0082 | 0.067696508  | 0.02162121    | 0.013446818 | 0.006022487 | 0.176370738      | 0.030803322 | 0.56          | 0.62           | 0.5          | 0.46        | 25.375   | 17.75176048 |
| Kenya              | 0.028 | 0.549660404  | 0.080825127   | 0.37075748  | 0.04755793  | 0.018599459      | 0.003098495 | 0.644444444   | 0.677777778    | 0.544444444  | 0.366666667 | 21.25    | 4.334248988 |
| Turkey             | 0.054 | 0.204893891  | 0.04031417    | 0.12121092  | 0.046782542 | 0.112578298      | 0.01789757  | 0.5           | 0.522222222    | 0.444444444  | 0.444444444 | 20       | 6.414269806 |
| Austria            | 0.0063 | 0.076583502  | 0.022920169   | 0.009906746 | 0.002457779 | 0.292369092      | 0.029833517 | 0.375         | 0.35           | 0.325        | 0.35        | 19.875   | 3.907410542 |
| Belgium            | 0.0081 | 0.113065355  | 0.020654221   | 0.011485014 | 0.002531384 | 0.270094859      | 0.029450338 | 0.5           | 0.6            | 0.5          | 0.5         | 19.75    | 7.005100183 |
| South Africa       | 0.039 | 0.251970045  | 0.046254482   | 0.278907287 | 0.065419443 | 0.068514271      | 0.004656853 | 0.518181818   | 0.536363636    | 0.390909091  | 0.5         | 19.125   | 8.659222994 |
| Jamaica            | 0.00203 | 0.169854429  | 0.073761877   | 0.090532081 | 0.013227793 | 0.056563603      | 0.011959155 | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 18.875   | 5.276294696 |
| Switzerland        | 0.0058 | 0.084950803  | 0.021977101   | 0.011468319 | 0.005498468 | 0.368427322      | 0.044613019 | 0.35          | 0.375          | 0.325        | 0.35        | 18.625   | 5.755432217 |
| Mexico             | 0.081 | 0.237222234  | 0.045196276   | 0.097608572 | 0.00865072  | 0.108356244      | 0.016132579 | 0.6           | 0.621428571    | 0.485714286  | 0.428571429 | 18       | 5.318431563 |
| Norway             | 0.00363 | 0.131127284  | 0.006976586   | 0.004615992 | 0.00106268  | 0.358138628      | 0.043847154 | 0.333333333   | 0.333333333    | 0.3          | 0.316666667 | 17.375   | 5.153015761 |
| Uzbekistan         | 0.021 | 0.301904019  | 0.0923144     | 0.214725196 | 0.033137168 | 0.0246702        | 0.006612288 | 0.45          | 0.425          | 0.35         | 0.5125      | 17.375   | 8.484229067 |
| Azerbaijan         | 0.0067 | 0.163812575  | 0.044615989   | 0.246142618 | 0.063028967 | 0.049111012      | 0.020558333 | 0.5           | 0.5            | 0.425        | 0.4375      | 16.625   | 9.620476674 |
| Argentina          | 0.030 | 0.220028535  | 0.03955074    | 0.069991244 | 0.002393544 | 0.119481932      | 0.014018854 | 0.423076923   | 0.469230769    | 0.338461538  | 0.453846154 | 16.375   | 2.973093627 |
| Croatia            | 0.0033 | 0.086537343  | 0.028709607   | 0.01984215  | 0.002485975 | 0.128100402      | 0.010873225 | 0.575         | 0.675          | 0.525        | 0.475       | 16.125   | 3.720119046 |
| Iran               | 0.056 | 0.189359397  | 0.102710898   | 0.120244856 | 0.01780251  | 0.074931158      | 0.005146098 | 0.4875        | 0.4125         | 0.325        | 0.5625      | 14.875   | 3.796144661 |
| Lithuania          | 0.0025 | 0.087116575  | 0.030847598   | 0.027400951 | 0.007212002 | 0.127200747      | 0.033259116 | 0.5           | 0.5            | 0.45         | 0.45        | 14.375   | 3.461523199 |
| India              | 0.88 | 0.294010269  | 0.073512791   | 0.346837568 | 0.037552085 | 0.018691567      | 0.006296145 | 0.468421053   | 0.484210526    | 0.373684211  | 0.384210526 | 14.25    | 7.887603293 |
| Finland            | 0.0040 | 0.117189979  | 0.008926824   | 0.001597927 | 0.001418522 | 0.250659485      | 0.017658153 | 0.333333333   | 0.266666667    | 0.266666667  | 0.3         | 14.125   | 6.599512969 |
| Georgia            | 0.0033 | 0.141725383  | 0.048486777   | 0.102141589 | 0.037345549 | 0.044866074      | 0.015792896 | 0.45          | 0.433333333    | 0.4          | 0.366666667 | 14       | 6.279217422 |
| North Korea        | 0.0185 | 0.154246424  | 0.018548323   | 0.177975503 | 0.051276668 | 0.009513198      | 0.003841105 | 0.34          | 0.3            | 0.3          | 0.28        | 13.875   | 6.937218463 |
| Colombia           | 0.032 | 0.197064849  | 0.055055283   | 0.096169531 | 0.00616974  | 0.065695975      | 0.007775463 | 0.644444444   | 0.677777778    | 0.544444444  | 0.366666667 | 13.625   | 8.034523721 |
| Slovakia           | 0.0041 | 0.079925955  | 0.040440331   | 0.027542455 | 0.002617979 | 0.124149981      | 0.018868687 | 0.466666667   | 0.433333333    | 0.4          | 0.433333333 | 13.625   | 6.300510183 |
| Slovenia           | 0.00155 | 0.075226347  | 0.040991715   | 0.006008882 | 0.002763456 | 0.175993035      | 0.008568691 | 0.5           | 0.5            | 0.45         | 0.45        | 13.5     | 3.207134903 |
| Thailand           | 0.050 | 0.101684257  | 0.023139534   | 0.072468391 | 0.010399325 | 0.074176045      | 0.007054593 | 0.775         | 0.825          | 0.725        | 0.225       | 13.375   | 4.068608046 |
| Indonesia          | 0.18 | 0.236168476  | 0.021017405   | 0.208448451 | 0.016437523 | 0.043063748      | 0.007524466 | 0.78          | 0.82           | 0.72         | 0.26        | 13.25    | 2.121320344 |
| Ethiopia           | 0.06 | 0.726952238  | 0.120769129   | 0.531948134 | 0.073077979 | 0.003402807      | 0.003166219 | 0.588888889   | 0.644444444    | 0.488888889  | 0.388888889 | 13.125   | 4.823676725 |
| Egypt              | 0.064 | 0.374207806  | 0.032766779   | 0.181378839 | 0.027679169 | 0.05040767       | 0.002975264 | 0.5           | 0.233333333    | 0.166666667  | 0.733333333 | 12.75    | 9.452890714 |
| Portugal           | 0.0079 | 0.069607163  | 0.016330427   | 0.013512546 | 0.004760622 | 0.180531069      | 0.025508225 | 0.6           | 0.7            | 0.5          | 0.45        | 12.625   | 5.153015761 |
| Mongolia           | 0.0020 | 0.263499279  | 0.076399013   | 0.200175936 | 0.077781058 | 0.037000874      | 0.012249351 | 0.266666667   | 0.183333333    | 0.166666667  | 0.4         | 12.25    | 6.11204899  |
| Algeria            | 0.026 | 0.316208925  | 0.075100438   | 0.157217748 | 0.015455829 | 0.056437161      | 0.00443705  | 0.5           | 0.36           | 0.24         | 0.64        | 10.75    | 2.434865793 |
| Ireland            | 0.0032 | 0.147326541  | 0.016645582   | 0.011347426 | 0.002502277 | 0.319672515      | 0.079709926 | 0.5           | 0.6            | 0.5          | 0.5         | 10.5     | 5.014265364 |
| Nigeria            | 0.12 | 0.739153142  | 0.023416376   | 0.822305082 | 0.107349622 | 0.020383944      | 0.002725677 | 0.65          | 0.55           | 0.45         | 0.45        | 10.375   | 3.814914341 |
| Serbia             | 0.0057 | 0.074177642  | 0.026628569   | 0.037869494 | 0.010891702 | 0.072838304      | 0.011948612 | 0.533333333   | 0.566666667    | 0.5          | 0.466666667 | 9.5      | 10.74376896 |
| Venezuela          | 0.020 | 0.250822403  | 0.039177642   | 0.10960241  | 0.053804729 | 0.09823887       | 0.040140459 | 0.642857143   | 0.657142857    | 0.528571429  | 0.371428571 | 9.375    | 3.335416016 |
| Armenia            | 0.0024 | 0.121849029  | 0.049211676   | 0.106752167 | 0.014767492 | 0.041279227      | 0.016043361 | 0.48          | 0.46           | 0.42         | 0.44        | 9.125    | 4.969550138 |
| Israel             | 0.0052 | 0.306177683  | 0.049126901   | 0.013760557 | 0.001360538 | 0.197047989      | 0.019334486 | 0.566666667   | 0.466666667    | 0.3          | 0.566666667 | 9        | 6.369570517 |
| Morocco            | 0.023 | 0.275078743  | 0.052033646   | 0.189452592 | 0.017488025 | 0.033320389      | 0.002876374 | 0.5           | 0.36           | 0.24         | 0.64        | 8.875    | 2.474873734 |
| Hong Kong China    | 0.0052 | 0.020911716  | 0.020326642   | 0.00169861  | 0.00097987  | 0.272159296      | 0.017689712 | 0.43125       | 0.45625        | 0.36875      | 0.35        | 8.5      | 3.927922024 |
| Estonia            | 0.0010 | 0.09095528   | 0.03097969    | 0.021071161 | 0.013054019 | 0.141608157      | 0.024261855 | 0.5           | 0.4            | 0.4          | 0.4         | 8.125    | 2.416461403 |
| Malaysia           | 0.020 | 0.230210046  | 0.077188316   | 0.034814382 | 0.00937092  | 0.110913243      | 0.010362403 | 0.95          | 0.95           | 0.9          | 0.15        | 7.625    | 3.583194903 |
| Tunisia            | 0.0079 | 0.195879508  | 0.052077122   | 0.116702382 | 0.017906104 | 0.050112802      | 0.001579733 | 0.5           | 0.36           | 0.24         | 0.64        | 7.625    | 5.153015761 |
| Latvia             | 0.0017 | 0.080198554  | 0.042802754   | 0.035452482 | 0.012830944 | 0.111945305      | 0.026144539 | 0.5           | 0.5            | 0.45         | 0.45        | 7.5      | 2.138089935 |
| Moldova            | 0.0029 | 0.120324679  | 0.039192359   | 0.104854359 | 0.016567354 | 0.045100297      | 0.013472683 | 0.533333333   | 0.566666667    | 0.5          | 0.466666667 | 6.125    | 3.720119046 |
| Bahamas            | 0.00026 | 0.151150963  | 0.047832062   | 0.05980047  | 0.008602429 | 0.209949567      | 0.052315016 | 0.7           | 0.7            | 0.6          | 0.3         | 5.625    | 2.065879266 |
| Dominican Republic | 0.0071 | 0.264191264  | 0.031746633   | 0.187112293 | 0.02969617  | 0.063387004      | 0.01249587  | 0.78          | 0.82           | 0.72         | 0.26        | 5.25     | 3.370036032 |
| Ecuador            | 0.011 | 0.271261663  | 0.061850549   | 0.109445637 | 0.015138275 | 0.051423237      | 0.006687484 | 0.65          | 0.7375         | 0.6          | 0.3125      | 4.875    | 4.086126353 |
| Trinidad and Tobago| 0.00104 | 0.117783843  | 0.025884998   | 0.116526095 | 0.022767947 | 0.124988884      | 0.017965754 | 0.8           | 0.8            | 0.7          | 0.25        | 4.75     | 2.604940361 |
| Kyrgyzstan         | 0.0041 | 0.31167292   | 0.05500734    | 0.176782825 | 0.02464987  | 0.021239321      | 0.00551735  | 0.375         | 0.3            | 0.2875       | 0.45        | 4.5      | 3.422613872 |
| Qatar              | 0.0010 | 0.248893527  | 0.097028931   | 0.0396375   | 0.002507345 | 0.483073915      | 0.063390306 | 0.6           | 0.2            | 0.1          | 0.8         | 3.5      | 0.9258201   |
| Philippines        | 0.068 | 0.355001499  | 0.07880694    | 0.174898718 | 0.033489789 | 0.030543401      | 0.004361407 | 0.76          | 0.86           | 0.7          | 0.2         | 2.75     | 2.121320344 |
| Cameroon           | 0.014 | 0.662789391  | 0.037122163   | 0.601139149 | 0.07036557  | 0.016028299      | 0.002298588 | 0.72          | 0.64           | 0.56         | 0.38        | 2.625    | 1.505940617 |
| Tajikistan         | 0.0056 | 0.411325611  | 0.066070704   | 0.3011951   | 0.051888249 | 0.010857464      | 0.005426467 | 0.4125        | 0.3875         | 0.325        | 0.4625      | 2.5      | 1.772810521 |
| Uganda             | 0.023 | 0.775649681  | 0.074798017   | 0.502831249 | 0.100300393 | 0.006098662      | 0.001844921 | 0.716666667   | 0.75           | 0.65         | 0.3         | 2.5      | 2.20389266  |
| Chile              | 0.0126 | 0.14054406   | 0.041510508   | 0.036271608 | 0.006562894 | 0.111587835      | 0.007868137 | 0.4125        | 0.3625         | 0.2875       | 0.525       | 2.25     | 1.281739889 |
| Cyprus             | 0.00080 | 0.103606981  | 0.047085505   | 0.009310672 | 0.004317767 | 0.19777133       | 0.01619569  | 0.55          | 0.6            | 0.4          | 0.45        | 2.125    | 1.246423455 |
| Pakistan           | 0.14 | 0.579391865  | 0.093251084   | 0.501427771 | 0.056970387 | 0.020817112      | 0.002885227 | 0.457142857   | 0.428571429    | 0.35         | 0.478571429 | 2.125    | 1.457737974 |
| Ghana              | 0.018 | 0.527285006  | 0.055234652   | 0.400744853 | 0.01952552  | 0.01756536       | 0.003746677 | 0.666666667   | 0.666666667    | 0.566666667  | 0.333333333 | 2        | 1.069044968 |
| Zimbabwe           | 0.0098 | 0.464024997  | 0.040637185   | 0.412922375 | 0.082830925 | 0.011059894      | 0.005608373 | 0.52          | 0.56           | 0.38         | 0.42        | 2        | 2.138089935 |
| Namibia            | 0.0015 | 0.442937418  | 0.057790356   | 0.296539626 | 0.045957542 | 0.046719206      | 0.005102021 | 0.45          | 0.25           | 0.175        | 0.7         | 1.875    | 1.125991626 |
| Vietnam            | 0.063 | 0.18916338   | 0.061301079   | 0.131304501 | 0.018910694 | 0.02862934       | 0.011164621 | 0.7           | 0.766666667    | 0.633333333  | 0.266666667 | 1.875    | 2.100170061 |
| Guatemala          | 0.010 | 0.440220965  | 0.120493289   | 0.205474888 | 0.008678545 | 0.040432462      | 0.005016516 | 0.7           | 0.8            | 0.66         | 0.26        | 1.75     | 1.281739889 |
| Kuwait             | 0.0020 | 0.238387884  | 0.068739998   | 0.042609051 | 0.007222398 | 0.321102182      | 0.075144724 | 0.6           | 0.2            | 0.1          | 0.8         | 1.75     | 1.281739889 |
| Zambia             | 0.010 | 0.682703645  | 0.056204822   | 0.552498745 | 0.087509291 | 0.01199601       | 0.00202393  | 0.5           | 0.65           | 0.45         | 0.325       | 1.75     | 1.669045921 |
| Botswana           | 0.0014 | 0.35171633   | 0.045996035   | 0.295061341 | 0.061968795 | 0.070632174      | 0.003884919 | 0.5           | 0.3            | 0.2          | 0.65        | 1.625    | 1.187734939 |
| Eritrea            | 0.0020 | 0.603933862  | 0.077361526   | 0.350891697 | 0.040559193 | 0.007179021      | 0.002959734 | 0.566666667   | 0.433333333    | 0.333333333  | 0.533333333 | 1.5      | 1.511857892 |
| Iceland            | 0.00023 | 0.162351409  | 0.015841205   | 0.00092465  | 0.001027511 | 0.268826245      | 0.01497927  | 0.25          | 0.3            | 0.25         | 0.25        | 1.5      | 1.069044968 |
| Albania            | 0.0023 | 0.154583738  | 0.066823733   | 0.079621101 | 0.019295008 | 0.046182542      | 0.01390888  | 0.55          | 0.6            | 0.475        | 0.45        | 1.375    | 1.060660172 |
| Turkmenistan       | 0.0040 | 0.316161311  | 0.052095864   | 0.336688456 | 0.040684947 | 0.055451341      | 0.02243817  | 0.475         | 0.4            | 0.275        | 0.6         | 1.375    | 1.505940617 |
| Montenegro         | 0.00047 | 0.137958993  | 0.02413669    | 0.027393071 | 0.014723333 | 0.084644879      | 0.007265722 | 0.575         | 0.625          | 0.5          | 0.45        | 1.25     | 1.488047618 |
| Angola             | 0.016 | 0.812826147  | 0.031345219   | 0.747520956 | 0.095061281 | 0.031051485      | 0.004975276 | 0.516666667   | 0.483333333    | 0.333333333  | 0.5         | 1.125    | 0.640869944 |
| Costa Rica         | 0.0032 | 0.175337306  | 0.061386459   | 0.043924131 | 0.009077669 | 0.087205348      | 0.007093522 | 0.775         | 0.8            | 0.725        | 0.275       | 1.125    | 1.125991626 |
| Ivory Coast        | 0.016 | 0.679470342  | 0.041038052   | 0.615232905 | 0.061670498 | 0.021108238      | 0.004953551 | 0.8           | 0.8            | 0.7          | 0.25        | 1.125    | 1.356202682 |
| Papua New Guinea   | 0.005 | 0.480090805  | 0.055572792   | 0.324323333 | 0.047673451 | 0.017764517      | 0.005826293 | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 1.125    | 0.83452296  |
| Tanzania           | 0.032 | 0.679032212  | 0.028743056   | 0.476147798 | 0.058246089 | 0.007177823      | 0.001967793 | 0.65          | 0.75           | 0.6          | 0.2875      | 1.125    | 1.642080562 |
| Uruguay            | 0.0025 | 0.167634992  | 0.02565958    | 0.053463645 | 0.003890575 | 0.102476139      | 0.011833916 | 0.55          | 0.65           | 0.55         | 0.5         | 1.125    | 0.83452296  |
| Iraq               | 0.022 | 0.544996078  | 0.06767867    | 0.185727426 | 0.021850976 | 0.039424076      | 0.009353191 | 0.5           | 0.44           | 0.34         | 0.5         | 1        | 1.309307341 |
| Mozambique         | 0.016 | 0.706263686  | 0.023159709   | 0.668694577 | 0.074922141 | 0.001566252      | 0.001817245 | 0.5           | 0.65           | 0.45         | 0.325       | 1        | 0.755928946 |
| Senegal            | 0.009 | 0.636731252  | 0.048343816   | 0.433099627 | 0.077438252 | 0.013597835      | 0.002197807 | 0.625         | 0.55           | 0.425        | 0.45        | 1        | 1.069044968 |
| Syria              | 0.014 | 0.419440917  | 0.086710815   | 0.095556045 | 0.015627197 | 0.033433793      | 0.014548147 | 0.5           | 0.4            | 0.283333333  | 0.616666667 | 1        | 1.069044968 |
| UAE                | 0.004 | 0.186742428  | 0.134323127   | 0.036687578 | 0.00697308  | 0.494866628      | 0.170660098 | 0.6           | 0.2            | 0.1          | 0.8         | 1        | 1.069044968 |
| Burundi            | 0.006 | 0.825107697  | 0.053460974   | 0.568262893 | 0.073181697 | 0.002101052      | 0.002172606 | 0.55          | 0.75           | 0.5          | 0.25        | 0.875    | 0.83452296  |
| Luxembourg         | 0.00037 | 0.098358253  | 0.01319814    | 0.004362246 | 0.001495961 | 0.584011546      | 0.026890196 | 0.5           | 0.6            | 0.5          | 0.5         | 0.875    | 0.83452296  |
| Peru               | 0.021  | 0.260459333  | 0.058286517   | 0.138275624 | 0.042340922 | 0.048330713      | 0.007731798 | 0.518181818   | 0.518181818    | 0.4          | 0.4         | 0.875    | 0.83452296  |
| Bosnia and Herzegovina | 0.0029 | 0.068885745  | 0.036228863   | 0.030782474 | 0.004087805 | 0.047546307      | 0.017678483 | 0.575         | 0.625          | 0.5          | 0.45        | 0.75     | 0.707106781 |
| Myanmar            | 0.0361 | 0.25078635   | 0.044963678   | 0.381200239 | 0.044449522 | 0.009660847      | 0.006591804 | 0.475         | 0.6            | 0.4375       | 0.2875      | 0.75     | 1.164964745 |
| Panama             | 0.0026 | 0.254367946  | 0.010871974   | 0.099985066 | 0.013207626 | 0.115968977      | 0.022260701 | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 0.75     | 0.88640526  |
| El Salvador        | 0.0046 | 0.251931322  | 0.087705978   | 0.117296572 | 0.021675927 | 0.03980804       | 0.003336152 | 0.7           | 0.7            | 0.6          | 0.3         | 0.625    | 0.916125381 |
| Nicaragua          | 0.0041 | 0.30103865   | 0.077850372   | 0.137175483 | 0.022901968 | 0.023175274      | 0.002010857 | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 0.625    | 0.744023809 |
| Saudi Arabia       | 0.0163 | 0.387758631  | 0.142541263   | 0.069220076 | 0.021743549 | 0.254454388      | 0.041940875 | 0.55          | 0.15           | 0.1          | 0.85        | 0.625    | 0.744023809 |
| Congo Dem. Rep.    | 0.05 | 0.85100422   | 0.056792475   | 0.68008459  | 0.052390534 | 0.002231575      | 0.002164587 | 0.85          | 0.875          | 0.775        | 0.2         | 0.5      | 0.755928946 |
| Fiji               | 0.00066 | 0.286708113  | 0.029128076   | 0.121405099 | 0.050730646 | 0.056813258      | 0.008103503 | 0.95          | 0.95           | 0.9          | 0.15        | 0.5      | 0.755928946 |
| Gabon              | 0.0012 | 0.51264883   | 0.043585507   | 0.347174078 | 0.033498453 | 0.091007801      | 0.028019389 | 0.85          | 0.875          | 0.775        | 0.2         | 0.5      | 0.755928946 |
| Honduras           | 0.0058 | 0.405013668  | 0.113103883   | 0.138542143 | 0.009533154 | 0.024623343      | 0.002818925 | 0.8           | 0.84           | 0.74         | 0.26        | 0.5      | 0.755928946 |
| Jordan             | 0.005 | 0.430001103  | 0.077131009   | 0.106319971 | 0.010698908 | 0.055964151      | 0.009010739 | 0.5           | 0.36           | 0.24         | 0.64        | 0.5      | 0.755928946 |
| Sudan              | 0.025 | 0.659525303  | 0.030730404   | 0.447729822 | 0.035247927 | 0.02046415       | 0.002228793 | 0.566666667   | 0.433333333    | 0.333333333  | 0.533333333 | 0.5      | 0.755928946 |
| Burkina Faso       | 0.011 | 0.762503443  | 0.065860348   | 0.687311573 | 0.060970736 | 0.005828702      | 0.001538851 | 0.566666667   | 0.433333333    | 0.333333333  | 0.533333333 | 0.375    | 0.51754917  |
| Lebanon            | 0.0037 | 0.233522068  | 0.034963187   | 0.059415716 | 0.012840242 | 0.080741693      | 0.011285829 | 0.6           | 0.7            | 0.5          | 0.45        | 0.375    | 0.51754917  |
| Paraguay           | 0.0041 | 0.336227078  | 0.081762069   | 0.138591238 | 0.014520692 | 0.059108587      | 0.007776975 | 0.62          | 0.68           | 0.56         | 0.36        | 0.375    | 0.51754917  |
| Sri Lanka          | 0.0152 | 0.191820269  | 0.014393462   | 0.061750157 | 0.026142628 | 0.045708496      | 0.010914541 | 0.9           | 0.933333333    | 0.833333333  | 0.166666667 | 0.375    | 0.51754917  |
| Djibouti           | 0.00064 | 0.459935547  | 0.12670673    | 0.430756683 | 0.04257445  | 0.017474601      | 0.004648464 | 0.5           | 0.3            | 0.2          | 0.65        | 0.25     | 0.46291005  |
| Guinea-Bissau      | 0.0011 | 0.661275244  | 0.069684282   | 0.697986277 | 0.029592815 | 0.006336712      | 0.001928954 | 0.75          | 0.8            | 0.65         | 0.25        | 0.25     | 0.46291005  |
| Guyana             | 0.00058 | 0.285131257  | 0.027259465   | 0.203939885 | 0.027983133 | 0.054769205      | 0.020142274 | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 0.25     | 0.46291005  |
| Haiti              | 0.0070 | 0.439887169  | 0.094272623   | 0.466008165 | 0.044587627 | 0.014544833      | 0.00350129  | 0.866666667   | 0.866666667    | 0.8          | 0.2         | 0.25     | 0.46291005  |
| Madagascar         | 0.015 | 0.63226249   | 0.070174291   | 0.430964172 | 0.032769334 | 0.006109842      | 0.001862862 | 0.625         | 0.725          | 0.5875       | 0.325       | 0.25     | 0.46291005  |
| Sierra Leone       | 0.0043 | 0.694068064  | 0.094840388   | 0.936841003 | 0.072812028 | 0.00478155       | 0.001706726 | 0.8           | 0.8            | 0.7          | 0.25        | 0.25     | 0.707106781 |
| Somalia            | 0.008 | 0.962061844  | 0.031002283   | 0.831743058 | 0.178032731 | 0.001985282      | 0.001425712 | 0.6           | 0.5            | 0.366666667  | 0.5         | 0.25     | 0.46291005  |
| Suriname           | 0.00039 | 0.270962116  | 0.015553317   | 0.135575128 | 0.006133796 | 0.09011896       | 0.013925132 | 0.95          | 0.95           | 0.9          | 0.15        | 0.25     | 0.46291005  |
| Togo               | 0.0047 | 0.622216336  | 0.030110522   | 0.518617688 | 0.045389445 | 0.007344175      | 0.001977384 | 0.7           | 0.7            | 0.6          | 0.3         | 0.25     | 0.46291005  |
| Bangladesh         | 0.109 | 0.288134108  | 0.079798091   | 0.318131869 | 0.067109496 | 0.01494896       | 0.005775828 | 0.7           | 0.766666667    | 0.633333333  | 0.266666667 | 0.125    | 0.353553391 |
| Benin              | 0.007 | 0.717537155  | 0.037816863   | 0.64250715  | 0.090819341 | 0.012424871      | 0.001834036 | 0.55          | 0.55           | 0.45         | 0.4         | 0.125    | 0.353553391 |
| Central African Republic | 0.0032 | 0.766754164  | 0.089066882   | 0.80868592  | 0.150714657 | 0.002847406      | 0.001497618 | 0.666666667   | 0.666666667    | 0.566666667  | 0.333333333 | 0.125    | 0.353553391 |
| Eswatini           | 0.00081 | 0.419229094  | 0.072797765   | 0.465036623 | 0.128347796 | 0.035636138      | 0.003305615 | 0.5           | 0.65           | 0.45         | 0.325       | 0.125    | 0.353553391 |
| Liberia            | 0.0027 | 0.659781761  | 0.068145642   | 0.686639518 | 0.129208273 | 0.004171454      | 0.002117319 | 0.8           | 0.8            | 0.7          | 0.25        | 0.125    | 0.353553391 |
| Mali               | 0.011 | 0.86491118   | 0.021429004   | 0.782023538 | 0.037461278 | 0.007355229      | 0.000901642 | 0.566666667   | 0.433333333    | 0.333333333  | 0.533333333 | 0.125    | 0.353553391 |
| Oman               | 0.0022 | 0.399762239  | 0.144967708   | 0.064915817 | 0.012503684 | 0.209526808      | 0.032060266 | 0.6           | 0.2            | 0.1          | 0.8         | 0.125    | 0.353553391 |
| Rwanda             | 0.007 | 0.637769346  | 0.115083344   | 0.487330953 | 0.190948036 | 0.004559076      | 0.002569982 | 0.533333333   | 0.7            | 0.5          | 0.333333333 | 0.125    | 0.353553391 |
| Solomon Islands    | 0.00039 | 0.547387018  | 0.04804122    | 0.130025396 | 0.021044614 | 0.011265644      | 0.004267144 | 1             | 1              | 1            | 0.1         | 0.125    | 0.353553391 |



#### 5.2.1 Corrélations entre Variables

Julien


#### 5.2.2 Analyse en Composantes Principales

Julien

#### 5.2.3 Sélection d'Attributs

Pour cette section, on va étudier l'importace de chaque attribut pour les tâches de classification et de régression. Pour ce faire, on va utiliser les méthodes les scores de F-test, Information mutuelle et On va corroborer nos résultas obtenus grâce à l'analyse des nouds d'un arbre de décision.

##### Test F :

Le test F est une méthode statistique utilisée pour déterminer si des variables explicatives (features) sont significativement liées à la variable cible dans des tâches supervisées, notamment la régression ou la classification. Grâce à ce test, on obtient un score F pour chaque attribut qui permet de mesurer l'importance de cet attribut pour la tâche en question. Plus le score F est élevé, plus l'attribut est important pour la tâche. Le score F mesure la relation linéaire entre les variables explicatives et la variable cible.


##### Information Mutuelle :

L'information mutuelle (MI) est une mesure issue de la théorie de l'information qui quantifie la dépendance entre deux variables aléatoires. En feature selection (sélection de variables), l'information mutuelle permet d'évaluer combien une variable explicative 
X réduit l'incertitude sur la variable cible Y. Contrairement au F-test, l'information mutuelle détecte aussi bien les relations linéaires que non linéaires. Plus le score d'information mutuelle est élevé, plus l'attribut est important pour la tâche.

Nous allons faire la distinction entre l'analyse des attributs pour la classification et pour la régression car les attributs importants peuvent différer selon la tâche.

##### Comparaison de Test F et MI

Nous allons faire la distinction entre l'analyse des attributs pour la classification et pour la régression car les attributs importants peuvent différer selon la tâche.

###### **1. Régression :**

| **Feature**        | **F-Score** | **MI-Score** | **Interprétation**                                   |
|--------------------|-------------|-------------|-----------------------------------------------------|
| **fertility**       | 205.11      | 0.33        | Très significative avec un bon MI-score.             |
| **pop**             | 148.74      | 0.29        | Forte relation linéaire et non linéaire.             |
| **capita**          | 147.52      | 0.24        | Significative mais légèrement plus faible en MI.     |
| **child**           | 142.81      | 0.29        | Indique une corrélation importante et non linéaire.  |
| **Avg_Temperature** | 106.67      | 0.42        | Relation non linéaire forte : le MI-score est élevé. |
| **Avg_Precipitation** | 34.36     | 0.38        | Relation moins linéaire, mais significative en MI.   |
| **Avg_Seasonality** | 17.66       | 0.40        | Relation non linéaire claire malgré un faible F-Score. |
| **Avg_Aridity**     | 0.09        | 0.37        | Le F-test la juge insignifiante, mais MI montre une contribution. |

**Observation :**
- Les variables comme **Avg_Temperature**, **Avg_Seasonality**, et **Avg_Aridity** ont des **F-Scores faibles** mais des **MI-Scores élevés**, indiquant des **relations non linéaires** avec la variable cible.
- La variable **fertility** est significative dans les deux méthodes.

###### **2. Classification :**

| **Feature**        | **F-Score** | **MI-Score** | **Interprétation**                                   |
|--------------------|-------------|-------------|-----------------------------------------------------|
| **fertility**       | 80.09       | 0.13        | Très significative linéaire, mais MI-score modéré.   |
| **child**           | 53.49       | 0.13        | Bonne dépendance linéaire et non linéaire.           |
| **capita**          | 52.11       | 0.11        | Significative dans les deux cas, mais faible en MI.  |
| **pop**             | 42.98       | 0.18        | Contribution plus forte en MI qu’en F-score.         |
| **Avg_Temperature** | 30.66       | 0.18        | Relation non linéaire, reflétée dans un MI-score plus élevé. |
| **Avg_Precipitation** | 9.20      | 0.20        | Peu linéaire (F-score faible) mais forte dépendance globale. |
| **Avg_Seasonality** | 4.21        | 0.19        | Contribution principalement non linéaire.            |
| **Avg_Aridity**     | 0.39        | 0.17        | Le F-score est insignifiant, mais MI montre une relation. |

**Observation :**
- Les variables comme **Avg_Temperature**, **Avg_Precipitation**, et **Avg_Seasonality** sont clairement **non linéaires** dans leur relation avec la classe des pays perfomants.
- La variable **fertility** reste une variable-clé dans les deux cas.

###### **Comparaison globale F-Test vs Information Mutuelle :**

| **Points clés**     | **F-Test**                             | **Information Mutuelle**                    |
|--------------------|----------------------------------------|---------------------------------------------|
| **Type de relation**| Détecte uniquement les relations linéaires. | Détecte les relations linéaires et non linéaires. |
| **Variables influentes** | Forte influence de **fertility**, **capita** | Influence non linéaire des variables climatiques. |
| **Faibles contributeurs** | **Avg_Aridity** ignorée par le F-test. | **Avg_Aridity** montre une contribution modérée. |

**Conclusion :**
Les variables comme Avg_Temperature, Avg_Seasonality, et Avg_Aridity présentent des dépendances principalement non linéaires, soulignées par des MI-Scores élevés malgré des F-Scores faibles. À l’inverse, des variables telles que fertility, pop, et capita montrent une forte influence sur les relations linéaires, avec des F-Scores significatifs. Les deux approches de sélection d'attributs sont complémentaires et permettent de mieux comprendre les relations entre les variables explicatives et la variable cible. 

Le F-Test est efficace pour détecter les relations linéaires, mais peut sous-estimer l’impact de certaines variables clés. L'Information Mutuelle (MI), quant à elle, capture des dépendances plus complexes et permet d’identifier des contributions souvent ignorées par le F-Test, comme pour Avg_Aridity.

On peut combiner les deux approches pour une sélection d'attributs plus robuste et complète, en particulier pour des tâches de classification et de régression où les relations peuvent être linéaires ou non linéaires.

##### Analyse des Noeuds d'un Arbre de Décision

Pour cette partie, nous allons entraîner un arbre de décision sur les données de classification et de régression pour analyser les attributs les plus importants. Les arbres de décision sont des modèles d'apprentissage supervisé qui permettent de visualiser et d'interpréter les relations entre les attributs et la variable cible. En analysant les noeuds de l'arbre, on peut identifier les attributs les plus discriminants pour la tâche en question.

###### Arbre de Décision pour la Régression :

Comme mentionné précédemment, nous allons corroborer les résultats obtenus avec le F-Test et l'Information Mutuelle en analysant les noeuds d'un arbre de décision pour la régression. L'arbre de décision permet de visualiser les attributs les plus importants pour prédire la variable cible (nombre d'athlète classé dans 10 premiers).

Après avoir entraîné l'arbre de décision, on a remarqué que la profondeur maximale de l'arbre de 3 permettait d'obtenir les meilleurs résultats (R2 = 0.65). Si on augmente la profondeur, l'arbre risque de sur-apprendre les données et de perdre en généralisation.

Voici l'arbre de décision obtenu pour la régression :

![Arbre de Décision](./figures/feature_selection/arbre-decision-reg.png)

On peut voir que le taux de fertilité (fertility) est le premier attribut utilisé pour diviser les données, suivi par le popultion (pop), et le Avg_Temperature et le pib par habitant (capita). Ces attributs sont cohérents avec les résultats obtenus par le F-Test et l'Information Mutuelle, qui ont montré que la fertilité et la population étaient des attributs importants pour la régression. L'arbre de décision confirme ces résultats en montrant que la fertilité est le facteur le plus discriminant pour prédire le nombre d'athlètes classés dans les 10 premiers.



##### 5.2.3.4 Importance des Attributs avec un Arbre de Décision


### 5.3 Méthodes Non Supervisées

#### 5.3.1 UMAP

#### 5.3.2 t-SNE

#### 5.3.3 PCA

#### 5.3.4 Isomap

#### 5.3.5 Carte auto-organisatrices (SOM)

Pour cette itération nous avons décidé d'utiliser un réseau de neurones SOM pour effectuer un clustering des pays. Nous avons décidé de fixer le nombre de clusters à 5. Les données d'entrée sont le dataset avec les 3 classes selon les seuils précédents.  

![img](figures/nsup/iter_5_som.png)

```python
Cluster to Country and Class Mapping:
Cluster (0, 0): 11 countries -> ['Great Britain', 'Luxembourg', 'Belgium', 'USA', 'Slovenia', 'Spain', 'Japan', 'Italy', 'Denmark', 'Netherlands', 'Ireland']
Class distribution in Cluster (0, 0): {0: 1, 1: 1, 2: 1}
Cluster (0, 1): 16 countries -> ['Ukraine', 'Hungary', 'Slovakia', 'Armenia', 'Romania', 'South Korea', 'Latvia', 'Estonia', 'Belarus', 'Turkey', 'Russia', 'Georgia', 'Peru', 'Poland', 'Czech Republic', 'Lithuania']
Class distribution in Cluster (0, 1): {0: 1, 1: 1}
Cluster (0, 2): 10 countries -> ['Hong Kong China', 'Austria', 'Iceland', 'Sweden', 'Switzerland', 'Canada', 'Norway', 'New Zealand', 'Finland', 'Germany']
Class distribution in Cluster (0, 2): {0: 1, 1: 1, 2: 1}
Cluster (0, 3): 6 countries -> ['Chile', 'Iran', 'Kazakhstan', 'Israel', 'Argentina', 'Uzbekistan']
Class distribution in Cluster (0, 3): {0: 1}
Cluster (0, 4): 5 countries -> ['Oman', 'Saudi Arabia', 'UAE', 'Kuwait', 'Qatar']
Class distribution in Cluster (0, 4): {0: 1}
Cluster (1, 0): 5 countries -> ['France', 'Cyprus', 'Australia', 'Croatia', 'Portugal']
Class distribution in Cluster (1, 0): {0: 1, 1: 1}
Cluster (1, 1): 10 countries -> ['Serbia', 'Lebanon', 'Mexico', 'Greece', 'Moldova', 'Albania', 'Bulgaria', 'Montenegro', 'Bosnia and Herzegovina', 'Uruguay']
Class distribution in Cluster (1, 1): {0: 1}
Cluster (1, 2): 2 countries -> ['India', 'China']
Class distribution in Cluster (1, 2): {0: 1, 1: 1}
Cluster (1, 3): 4 countries -> ['Kyrgyzstan', 'Mongolia', 'North Korea', 'Tajikistan']
Class distribution in Cluster (1, 3): {0: 1}
Cluster (1, 4): 10 countries -> ['Jordan', 'Namibia', 'Morocco', 'Djibouti', 'Turkmenistan', 'Egypt', 'Algeria', 'Botswana', 'Syria', 'Tunisia']
Class distribution in Cluster (1, 4): {0: 1}
Cluster (2, 0): 4 countries -> ['Costa Rica', 'Trinidad and Tobago', 'Thailand', 'Cuba']
Class distribution in Cluster (2, 0): {0: 1, 1: 1}
Cluster (2, 1): 6 countries -> ['Paraguay', 'Venezuela', 'Bahamas', 'Brazil', 'Colombia', 'El Salvador']
Class distribution in Cluster (2, 1): {0: 1}
Cluster (2, 2): 4 countries -> ['Myanmar', 'Eswatini', 'Azerbaijan', 'South Africa']
Class distribution in Cluster (2, 2): {0: 1}
Cluster (2, 3): 2 countries -> ['Pakistan', 'Zimbabwe']
Class distribution in Cluster (2, 3): {0: 1}
Cluster (2, 4): 3 countries -> ['Iraq', 'Eritrea', 'Sudan']
Class distribution in Cluster (2, 4): {0: 1}
Cluster (3, 0): 5 countries -> ['Dominican Republic', 'Indonesia', 'Guatemala', 'Honduras', 'Vietnam']
Class distribution in Cluster (3, 0): {0: 1}
Cluster (3, 1): 3 countries -> ['Ecuador', 'Bangladesh', 'Philippines']
Class distribution in Cluster (3, 1): {0: 1}
Cluster (3, 2): 3 countries -> ['Kenya', 'Ghana', 'Madagascar']
Class distribution in Cluster (3, 2): {0: 1}
Cluster (3, 3): 6 countries -> ['Zambia', 'Senegal', 'Ethiopia', 'Mozambique', 'Rwanda', 'Burundi']
Class distribution in Cluster (3, 3): {0: 1}
Cluster (3, 4): 4 countries -> ['Mali', 'Angola', 'Somalia', 'Burkina Faso']
Class distribution in Cluster (3, 4): {0: 1}
Cluster (4, 0): 8 countries -> ['Panama', 'Sri Lanka', 'Fiji', 'Malaysia', 'Guyana', 'Suriname', 'Jamaica', 'Solomon Islands']
Class distribution in Cluster (4, 0): {0: 1}
Cluster (4, 1): 4 countries -> ['Nicaragua', 'Gabon', 'Papua New Guinea', 'Haiti']
Class distribution in Cluster (4, 1): {0: 1}
Cluster (4, 2): 5 countries -> ['Sierra Leone', 'Congo Dem. Rep.', 'Guinea-Bissau', 'Ivory Coast', 'Liberia']
Class distribution in Cluster (4, 2): {0: 1}
Cluster (4, 3): 5 countries -> ['Uganda', 'Togo', 'Central African Republic', 'Tanzania', 'Cameroon']
Class distribution in Cluster (4, 3): {0: 1}
Cluster (4, 4): 2 countries -> ['Nigeria', 'Benin']
Class distribution in Cluster (4, 4): {0: 1}
```

Après plusieurs essais nous avons pu obtenir une carte de 5x5 clusters avec un entrainement de 1000 itérations. Le clustering nous parait pas parfait néanmoins nous pouvons remarquer que la plupart des pays de classe 0 se retrouvent bien ensemble ainsi que les pays de classe 1. En ce qui concerne les pays de classe 2 ceux-ci sont dans le neurone de sortie # (0,0) et (0,2). Ceci est pertinent car ces pays sont ceux qui ont les meilleures performances. Ils bien séparés des autres pays. Nous remarquons également que nous trouvons des pays de memes régions géographique souvent dans le même cluster.

### 5.2 Méthodes Supervisées

#### 5.2.1 Arbre de Décision pour la classification

#### 5.2.2 Forêts Aléatoires

##### 5.2.2.1 Classification

##### 5.2.2.2 Régression

#### 5.2.3 XGBoost

##### 5.2.3.1 Classification

##### 5.2.3.2 Régression

#### 5.2.4 Réseaux de Neurones

##### 5.2.4.1 Baseline pour la Régression
Le premier modèle développé dans le cadre du projet était une régression linéaire simple appliquée sur le dataset de 1992, visant à établir une relation linéaire entre les variables socio-économiques et les performances olympiques. Les métriques de performance utilisées étaient le RMSE (Root Mean Squared Error) et l'optimiseur adam ainsi que le r^2 de Pearson pour l'évaluation.
![img](figures/sup/iter_1_model.png)
![img](figures/sup/iter_1_mes.png)
![img](figures/sup/iter_1_regression.png)
Notre premier modèle sert de baseline pour la suite de notre projet. Il nous permet de voir les améliorations que nous pouvons apporter. Un R^2 de 0.58 est relativement médiocre en revanche nous pouvons voir que le mlp est capable d'apprendre des caractéristiques d'après la courbe d'apprentissage.

#### 5.2.2 Itération 2 : Modèle de Régression Linéaire avec dataset complet
Dans cette deuxième itération, nous avons décidé d'ajouter des variables explicatives supplémentaires pour améliorer la performance de notre modèle. Les métriques de performance utilisées étaient le RMSE et le R^2 de Pearson pour l'évaluation.
![img](figures/sup/iter_2_model.png)
![img](figures/sup/iter_2_mse.png)
![img](figures/sup/iter_2_regression.png)
Nous constatons qu'en ajoutant plus de variables explicatives, notre modèle a une meilleure performance. En effet, le R^2 de Pearson passe de 0.58 à 0.87. Cela signifie que 87% de la variance de notre variable cible est expliquée par nos variables explicatives. Cependant nous pouvons voir que dans le coin gauche du bas nous avons un grand nombre de pays qui ne sont pas forcément bien traité par notre modèle.

### 5.2.3 Itération 3 : Modèle de Régression Linéaire avec deux branches

Dans cette itération nous avons décidé de construire un modèle de prédiction plus complexe. Une branche pour effectuer une classification selon la performance du pays et une autre qui se chargera de la régression. Les métriques restent les mêmes que pour les itérations précédentes. Nous attendons un granularité plus fine de ce modèle.

Nous commencerons par traiter 2 classes pour la branche concernée.

![img](figures/sup/iter_3_model.png)
![img](figures/sup/iter_3_loss.png)
![img](figures/sup/iter_3_mse.png)
![img](figures/sup/iter_3_acc.png)
![img](figures/sup/iter_3_conf.png)
![img](figures/sup/iter_3_reg.png)
Nous pouvons voir en premier lieu que notre modèle est capable de classifier les pays en 2 classes selon la performance du pays nous avons fixé le seuil à 0.3. Après normalisation des valeurs des performance des délégations si le pays à une performance < 0.3 alors il est marqué comme un pays de classe 0 sinon 1. A noter que les données des performances correspondent aux nombres d'athlètes faisant partie du top 10 pour les disciplines retenues pour chaque éditions. 

Nous pouvons en premier lieu de constater que le modèle est capable de classifier les pays selon les classes qui leur ont été assignées. En effet, l'accuracy semble bien augmenter au fil de l'entrainement. Nous obtenons un score f1 de 0.9085 et une accuracy de 0.93. La matrice de confusion nous permet de confirmer ces résultats relativement bons.

Concernant la régression nous ne pouvons pas en dire autant. Il semble que le réseau est capable de diminuer son loss selon l'entrainement mais la MSE ne semble pas diminuer. Nous observons plutot une courbe erratique. 
A noter que nous avons du considérablement augmenter le nombre de neurones pour la branche de la régression. Dans le cas contraire le modèle semblait être perturbé par la backpropagation de la classification.

### 5.2.4 itération 4 : Modèle de Régression Linéaire avec deux branches et 3 classes
Dans cette itération nous proposons de passer à 3 classes pour la classification. Nous avons décidé de classer les pays en 3 classes selon leur performance. Les métriques restent les mêmes que pour les itérations précédentes. Nous attendons un granularité plus fine de ce modèle. Les seuils sont fixés à 0.2 et 0.8 pour la définition des classes de pays.

![img](figures/sup/iter_4_model.png)
![img](figures/sup/iter_4_loss_reg.png)
![img](figures/sup/iter_4_loss_cl.png)
![img](figures/sup/iter_4_mse.png)
![img](figures/sup/iter_4_acc.png)
![img](figures/sup/iter_4_conf.png)
![img](figures/sup/iter_4_reg.png)

Nous observons un loss, autant sur la sortie de la régression que sur la classification qui démontre une bonne stabilité semblant capturer correctement des caractéristiques. La MSE de la régression cette fois est stable pour tous les folds et semble démonter un apprentissage également. Concernant l'accuracy nous obtenons une courbe plus cohérente dans le sens que les oscillations restent stables et semblent converger vers une meilleur résultat ~0.87. Nous obtenons un F1 de 0.90 pour la classification en 3 classes.

L'analyse du R^2 est plutôt satisfaisant nous arrivons avec un coefficient de Pearson de 0.77 alors que le modèle en 2 classes était négatif. Nous n'atteignons pas le 0.87 du modèle de l'itération 2 mais nous sommes capable de classifier les pays avec le modèle actuel. La classification influence certainement la performance de la régression c'est probablement pourquoi nous ne sommes pas aussi bon que le modèle de l'itération 2. 

A noter qu'en comparaison avec l'itération précédente, nous avons environ 4000 paramètres avec le modèle actuel. Le modèle précédent demandait l'ajout de multiples couches pour la régression ce qui nous conduisait à avoir environ 68300 paramètres. La passage avec un nombre de classes plus granuleux permet certainement au modèle de mieux comprendre le comportement des performance et d'adapter son échelle de prédiction.

---
## 6. Résultats et Analyse
### 6.1 Performances des Modèles
- Présentation des métriques comme F1-score, précision, et RMSE.
- Comparaison des performances entre approches supervisées et non supervisées.

### 6.2 Insights Clés
- Identification des facteurs clés influençant les performances olympiques.
- Analyse des clusters régionaux et des tendances générales.




## 8. Discussion et améliorations
### 8.1 Forces et Faiblesses
- Points forts du projet 
- Limites rencontrées

### 8.2 Améliorations
- Intégration de nouvelles variables.
- Exploration d’approches de modélisation plus avancées.


## 9. Conclusion

## 10. Références

[1] https://www.kaggle.com/datasets/piterfm/olympic-games-medals-19862018?select=olympic_medals.csv

## 10. Annexes
### 10.1 Journal de Travail

