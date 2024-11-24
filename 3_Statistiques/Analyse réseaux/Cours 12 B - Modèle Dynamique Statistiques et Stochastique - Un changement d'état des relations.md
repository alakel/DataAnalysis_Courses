## Cours Théorique sur les Modèles Dynamiques Statistiques en Analyse de Réseau

L'analyse des réseaux dynamiques s'appuie sur des modèles statistiques avancés pour comprendre les évolutions structurelles dans le temps. Ces modèles capturent des processus relationnels tels que la formation, la dissolution et la transformation des liens entre nœuds, en intégrant souvent les attributs des acteurs et le contexte. Au fil du temps, plusieurs approches ont été développées, parmi lesquelles les **SAOM** (Stochastic Actor-Oriented Models), les **TERGM** (Temporal Exponential Random Graph Models), et les **HMM** (Hidden Markov Models for Network Evolution). Ce cours explore la généalogie et le fonctionnement de ces modèles, tout en soulignant leurs contributions et leurs limites dans la compréhension des réseaux évolutifs.

Dans les réseaux dynamiques, les relations ne sont pas statiques ; elles changent en fonction du comportement des individus, des événements contextuels, ou des conditions externes. Les **modèles dynamiques** sont conçus pour :

1. **Comprendre les mécanismes d'évolution des liens** : Comment et pourquoi certains liens se forment, persistent, ou se dissolvent dans le temps.
2. **Analyser l'impact des attributs des nœuds** : Par exemple, observer comment des caractéristiques individuelles (statut social, popularité) influencent les tendances relationnelles.
3. **Étudier la dépendance temporelle** : Savoir si les relations passées influencent les relations futures, et dans quelle mesure.

Ces modèles sont largement appliqués en **sociologie**, **épidémiologie**, **science des organisations**, et **analyse de réseaux sociaux en ligne**.
# I. Généalogie et Types de Modèles Dynamiques Statistiques en Réseaux

Les modèles dynamiques sont issus de la combinaison des théories des réseaux avec des méthodes statistiques permettant de modéliser des processus dépendant du temps. Nous examinerons ici les principales familles de modèles dynamiques, leur fonctionnement, et leurs spécificités.
## 1.1 Modèles Stochastiques Basés sur les Acteurs : SAOM

Les **Stochastic Actor-Oriented Models (SAOM)**, introduits par **Snijders (2001)**, modélisent les réseaux comme le résultat d’un processus stochastique où les acteurs (nœuds) prennent des décisions individuelles. Ils reposent sur le cadre des **chaînes de Markov Monte Carlo (MCMC)**, permettant de modéliser chaque changement de lien à chaque étape temporelle en fonction des préférences des acteurs et des caractéristiques du réseau.

1. **Fonctionnement et Algorithme** : Les SAOM reposent sur l’idée que les acteurs prennent des décisions sur la base de la configuration actuelle du réseau et de leurs préférences individuelles. L'algorithme se déroule en étapes :
   - Les acteurs évaluent leurs relations actuelles et potentielles.
   - Ils prennent des décisions de manière itérative pour créer ou supprimer des liens.
   - L’ensemble des actions est simulé en chaîne de Markov, permettant de capturer la dépendance temporelle des liens.

2. **Spécificités et Apports** :
   - Modélisation des **décisions individuelles** : Les SAOM capturent les processus individuels de formation et dissolution de liens, en intégrant les préférences et contraintes de chaque acteur.
   - Adapté aux **réseaux d’amitié**, **réseaux professionnels**, et **réseaux de groupe**, les SAOM permettent d'explorer comment des caractéristiques comme l'âge, le sexe, ou le statut influencent les interactions.
   
3. **Applications** :
   - Étude des réseaux d’amitié en milieu scolaire pour observer comment les élèves forment des groupes.
   - Analyse des réseaux organisationnels pour comprendre les processus de création de sous-groupes.

> [!NOTE]
> **Références**
> **Snijders, T. A. B. (2002).** The statistical evaluation of social network dynamics. _Sociological Methodology_, 31(1), 361–395. [Voir](https://doi.org/10.1111/0081-1750.00099)

## 1.2 Modèles ERGM Temporels : TERGM

Les **Temporal Exponential Random Graph Models (TERGM)**, développés par **Hanneke, Fu, et Xing (2010)**, sont une extension des modèles ERGM qui ajoutent la dimension temporelle pour prendre en compte la persistance et l’évolution des liens.

1. **Fonctionnement et Algorithme** :
   - Les TERGM supposent que les configurations passées influencent les relations futures, permettant ainsi une dépendance temporelle explicite.
   - À chaque point temporel, un réseau est modélisé en fonction des structures observées précédemment, en utilisant une **distribution exponentielle** pour capturer la probabilité de chaque lien en fonction des motifs passés.

2. **Spécificités et Apports** :
   - Permet de modéliser des effets temporels sur la formation des liens, comme la **stabilité relationnelle** ou la **propension des triades à se fermer** au fil du temps.
   - Adapté pour les réseaux **d’interaction en ligne**, **réseaux de citations**, ou **réseaux professionnels** où la structure évolue à chaque étape.

3. **Applications** :
   - Analyse des réseaux de communication évolutifs pour observer comment les relations de collaboration persistent ou changent.
   - Étude des réseaux de citations académiques pour modéliser les tendances de citation au fil du temps.

> [!NOTE]
> Hanneke, S., Fu, W., & Xing, E. P. (2010). Discrete temporal models of social networks. _Electronic Journal of Statistics_, 4, 585-605. [Voir](https://projecteuclid.org/journals/electronic-journal-of-statistics/volume-4/issue-none/Discrete-temporal-models-of-social-networks/10.1214/09-EJS548.full)

## 1.3 Approches Bayésiennes pour Modèles Dynamiques de Réseau

Les **Hidden Markov Models for Network Evolution (HMNE)**, ou **modèles de Markov cachés** pour l'évolution des réseaux, reposent sur la notion d'**état latent**, qui représente des informations sous-jacentes, non directement observables dans le réseau. Les états latents influencent les transitions et les relations entre les nœuds du réseau, mais ces états ne sont pas directement mesurés ; ils doivent être **inférés** à partir des données observées. Cette idée de **"caché"** est centrale pour les modèles de Markov cachés (HMM) en général, et les HMNE en sont une application spécifique dans les réseaux.

**Concepts de Base : États Latents et Observables**

- **État latent** : Dans le contexte des HMNE, un état latent représente des caractéristiques ou des attributs internes d’un nœud ou d’un lien qui influencent leur comportement ou leurs connexions dans le réseau, mais qui ne sont pas directement visibles. Par exemple, un état latent pourrait indiquer une préférence d'un acteur pour se connecter à des groupes particuliers ou une tendance à influencer d'autres nœuds.

- **État observable** : Les états observables sont les relations visibles dans le réseau, telles que la présence ou l’absence de liens entre nœuds.

**Structure des HMM et Rôle des États Latents dans les HMNE**

Les modèles de Markov cachés fonctionnent en utilisant deux processus interdépendants :

1. **Processus de transition entre les états latents** : Un nœud peut passer d'un état latent à un autre selon une probabilité définie par une matrice de transition. Cette matrice indique les probabilités de transition entre les états latents d'un pas de temps à l'autre.

2. **Processus d'émission d'états observables** : À partir de chaque état latent, des états observables sont générés selon une probabilité. Par exemple, si un nœud est dans un état latent de « forte influence », il peut avoir une probabilité plus élevée d’émettre des liens vers d’autres nœuds.

Dans le cadre des HMNE, ces deux processus permettent de modéliser comment la structure du réseau évolue au fil du temps en fonction des états latents des nœuds. Cela signifie que la structure du réseau observable à chaque moment est influencée par une configuration d’états latents.

**Calcul des États Latents : L’Algorithme de Baum-Welch et la Méthode de Filtrage**

Pour calculer les états latents dans les HMNE, deux méthodes principales sont utilisées :

**a) L'algorithme de Baum-Welch**
Cet algorithme permet d'inférer les paramètres du modèle (probabilités de transition et d'émission) en fonction des données observées :

1. **Étape d'initialisation** : On initialise les probabilités de transition et d'émission avec des valeurs hypothétiques.
2. **Étapes itératives de correction** : À chaque itération, on ajuste les probabilités de transition et d’émission pour maximiser la probabilité des données observées.
3. **Convergence** : On arrête les itérations lorsque les paramètres convergent vers une solution stable.

**b) L'algorithme de filtrage (ou Forward-Backward)**
Cet algorithme est utilisé pour estimer les états latents au sein du modèle une fois les paramètres déterminés. Il comporte deux étapes :

1. **Phase Forward (avancer)** : En se basant sur les observations passées et sur les probabilités de transition, on estime la probabilité d'être dans un état latent donné à un moment précis.
2. **Phase Backward (retour)** : En revenant en arrière dans la séquence, on met à jour cette estimation en fonction des observations futures.

En combinant ces étapes, on obtient une séquence d’estimations pour les états latents des nœuds à chaque moment du temps.

**Logique et Applications des États Latents dans les Réseaux**

Les HMNE permettent d’analyser des réseaux en capturant des dynamiques cachées. Par exemple, dans un réseau de collaboration, les états latents peuvent représenter l’intérêt sous-jacent des chercheurs pour collaborer sur certains types de projets, même si cet intérêt n’est pas directement observable. En inférant ces états, les chercheurs peuvent :

- Identifier les périodes où un acteur était « influent » ou « marginal » sans que cela soit explicitement visible.
- Détecter des changements de dynamique dans le réseau, tels que la formation ou la dissolution de groupes.
- Analyser des transitions dans les préférences de connexion d’un acteur, ce qui peut indiquer des changements stratégiques ou organisationnels.

Les HMNE, et plus largement les HMM, permettent de modéliser des réseaux évolutifs en intégrant des couches d’information non observables (états latents). L'algorithme de Baum-Welch est utilisé pour ajuster les paramètres du modèle, tandis que l'algorithme de filtrage permet d’estimer les états latents des nœuds. Ces états latents offrent une vue approfondie sur les mécanismes cachés qui influencent l'évolution des réseaux, rendant les HMNE particulièrement puissants pour des réseaux avec des changements fréquents ou des dynamiques complexes.

> [!NOTE]
> **Référence**
> Krivitsky, P. N., & Handcock, M. S. (2014). A Separable Model for Dynamic Networks. _Journal of the Royal Statistical Society Series B: Statistical Methodology_, _76_(1), 29‑46. [Voir](https://doi.org/10.1111/rssb.12014)

## 1.4 Approches Bayésiennes pour Modèles Dynamiques de Réseau

Le **btergm** est conçu pour modéliser l'évolution des réseaux dans le temps en s'appuyant sur les modèles de réseaux exponentiels temporels, ou **TERGM**. Voici les fondements théoriques de ce modèle, expliqués pour une compréhension approfondie.

**Extension des ERGM aux données longitudinales**

Les **TERGM** sont une extension des ERGM, initialement développés pour modéliser des réseaux statiques (sans changement au fil du temps). Avec les TERGM, l’objectif est de comprendre comment un réseau évolue, en prenant en compte son état passé pour prédire son état futur. En d’autres termes, le TERGM permet de modéliser comment les liens entre les nœuds changent d’une période à l'autre en fonction des relations observées précédemment, capturant ainsi les dynamiques temporelles.

**Méthodologie d'Estimation**

Pour estimer les paramètres dans un modèle TERGM, **btergm** utilise une méthode appelée **pseudovraisemblance maximale** combinée avec des **intervalles de confiance bootstrap** :

- **Pseudovraisemblance** : Plutôt que de calculer la vraisemblance totale du réseau (ce qui est très coûteux en termes de calcul), la pseudovraisemblance évalue la probabilité de chaque lien en le conditionnant sur les autres liens du réseau. Cela rend l'estimation plus rapide, particulièrement pour les réseaux de grande taille.
- **Bootstrap** : Comme la pseudovraisemblance peut biaiser les résultats, les auteurs ajoutent une méthode de bootstrap pour corriger ce biais. Cette technique consiste à rééchantillonner les données plusieurs fois pour estimer les intervalles de confiance, assurant ainsi des estimations plus fiables des paramètres dans les analyses longitudinales.

**Termes de Mémoire et Dépendances Temporelles**

Le **btergm** utilise des "termes de mémoire" pour tenir compte des dépendances temporelles, c’est-à-dire des effets des liens passés sur les liens futurs. Ces termes incluent notamment :
- **Persistance des liens** : Un lien formé à un moment donné a tendance à persister dans le temps.
- **Stabilité dyadique** : La probabilité qu’un lien continue d’exister entre deux nœuds au fil du temps.

Ces termes de mémoire permettent de mieux comprendre comment certains liens se renforcent ou se dissolvent, offrant une vision plus fine de la stabilité et des changements dans les réseaux au cours du temps.

**Utilisation des Covariables Exogènes et Endogènes**

Les TERGM peuvent également intégrer des covariables pour enrichir les analyses :
- **Covariables exogènes** : Ces attributs proviennent de caractéristiques externes aux nœuds (comme le genre, l’âge) et influencent la formation de liens entre eux.
- **Covariables endogènes** : Elles incluent des attributs qui dépendent des liens existants dans le réseau, comme la réciprocité différée (tendance à ce qu’un nœud réponde à un lien dans le futur).

En combinant les termes de mémoire et les covariables, les TERGM permettent de capturer des effets temporels complexes et de modéliser les processus de formation de liens de manière plus détaillée. Ils sont particulièrement utiles dans des contextes où les réseaux sont dynamiques, comme les réseaux de communication ou d’amitié, et où l’évolution des relations peut révéler des tendances importantes dans la structure globale du réseau. 

> [!NOTE]
> Leifeld, P., Cranmer, S. J., & Desmarais, B. A. (2018). Temporal Exponential Random Graph Models with btergm : Estimation and Bootstrap Confidence Intervals. _Journal of Statistical Software_, _83_, 1‑36. [Voir](https://doi.org/10.18637/jss.v083.i06)

##2 Analyse dynamique de réseau dans R

# II. Implémentation des Modèles Dynamiques en R

## 2.1 Préparation des Données

Ce code permet de préparer les données en découpant les liens temporels en plusieurs périodes pour créer un réseau dynamique adapté aux modèles SAOM. Nous chargeons les nœuds et les liens à partir des fichiers `nodes.csv` et `links.csv` et découpons les liens en périodes définies par l'utilisateur.

```r
# Installation et chargement des packages nécessaires
install.packages(c("readr", "igraph", "RSiena"))
library(readr)   # Pour lire les fichiers CSV
library(igraph)  # Pour manipuler les réseaux
library(RSiena)  # Pour implémenter les modèles SAOM

# Fonction pour découper le réseau en périodes temporelles
split_network <- function(nodes_file, links_file, n_periods) {
    # Chargement des fichiers de nœuds et de liens
    nodes <- read_csv(nodes_file)
    links <- read_csv(links_file)
    
    # Conversion de la colonne 'date' en format Date pour faciliter la gestion temporelle
    links$date <- as.Date(links$date, format="%Y-%m-%d")
    
    # Calcul de la durée de chaque période
    first_date <- min(links$date)
    last_date <- max(links$date)
    period_length <- as.numeric(last_date - first_date) / n_periods
    
    # Création d'une liste pour stocker les réseaux de chaque période
    networks <- list()
    for(i in 1:n_periods) {
        # Définition des dates de début et de fin pour la période courante
        start_date <- first_date + (i-1)*period_length
        end_date <- start_date + period_length
        period_links <- links[links$date >= start_date & links$date < end_date, ]
        
        # Création du graphe pour la période courante
        g <- graph_from_data_frame(d=period_links, vertices=nodes, directed=TRUE)
        networks[[i]] <- g
    }
    
    return(networks)  # Retourne la liste de réseaux pour chaque période
}

# Utilisation de la fonction pour diviser le réseau en périodes
nodes_file <- "nodes.csv"  # Nom du fichier de nœuds
links_file <- "links.csv"  # Nom du fichier de liens
n_periods <- 5             # Nombre de périodes à définir
networks <- split_network(nodes_file, links_file, n_periods)
```

## 2.2. Modélisation de SOAM avec RSiena

Une fois les réseaux découpés en périodes, nous passons à l'étape de modélisation SAOM avec le package **RSiena**. Dans ce modèle, nous spécifions des effets en fonction des caractéristiques des nœuds, telles que le genre et l'âge.

#### Code pour le Modèle SAOM avec RSiena

```r
# Préparation des données pour RSiena
# Conversion des réseaux en matrices d'adjacence pour chaque période
friendship <- sienaNet(array(lapply(networks, function(net) as.matrix(as_adjacency_matrix(net))), 
                           dim=c(vcount(networks[[1]]), vcount(networks[[1]]), n_periods)))

# Ajout de variables individuelles en tant que covariables (âge et genre)
# Attention : les variables 'age' et 'gender' doivent être présentes dans le fichier nodes.csv
age <- coCovar(nodes$age)        # Covariable pour l'âge
gender <- coCovar(nodes$gender)  # Covariable pour le genre

# Création de l'objet de données pour RSiena
mydata <- sienaDataCreate(friendship, age, gender)

# Définition des effets pour le modèle
# Spécification des effets pour le modèle 
					   
effects <- getEffects(my_data) effects <- includeEffects(effects, density) # Effet de densité 
effects <- includeEffects(effects, recip) # Effet de réciprocité 
effects <- includeEffects(effects, transTrip) # Effet de transitivité 
effects <- includeEffects(effects, sameX, interaction1="gender") # Effet d'homophilie (genre)

# Création et paramétrage du modèle
model1 <- sienaModelCreate(useStdInits = TRUE, projname = "friendship_model")

# Estimation des paramètres avec RSiena (peut prendre du temps pour des réseaux de grande taille)
# Il est possible d'ajuster le nombre d'itérations en fonction des besoins
result <- siena07(model1, data=mydata, effects=effects)

# Affichage des résultats 
summary(results) # Extraire les coefficients pour interprétation des odd ratios 
coef_estimates <- results$theta # Calcul des odd ratios pour chaque effet 
odd_ratios <- exp(coef_estimates) 
names(odd_ratios) <- results$effects$effectName print(odd_ratios)

```
### Explications et Améliorations pour Chaque Partie du Code

Voici une liste complète des effets que vous pouvez inclure avec la fonction `includeEffects()` dans RSiena. Cette liste couvre les principaux effets utilisés dans les analyses de réseaux sociaux dynamiques avec le SAOM.

### Effets de base

- `density` : Effet de densité, représente la tendance générale des nœuds à former des liens.
- `recip` : Effet de réciprocité, modèle la tendance des nœuds à créer des liens réciproques.
- `transTrip` : Effet de transitivité, capture la formation de triangles (liens fermés) dans le réseau.
- `balance` : Effet d'équilibre, tendance à former des liens avec des amis d'amis (similaire à la transitivité).

### Effets d'homophilie et d'attraction

- `sameX` : Homophilie par attribut, modélise la tendance des nœuds partageant un attribut commun (par exemple, genre) à se connecter.
- `altX` : Effet d'attractivité d’un attribut exogène, montre l'influence d'une covariable exogène sur l'attractivité des nœuds.
- `egoX` : Effet d’ego d’un attribut, examine l'influence d'une covariable exogène sur la propension d'un nœud à envoyer des liens.
- `simX` : Similarité, modélise la probabilité de lien en fonction de la similarité entre les attributs des nœuds.

### Effets de popularité et d'activité

- `indegree` : Effet de popularité, modélise la tendance des nœuds ayant beaucoup de liens entrants à recevoir davantage de liens.
- `outdegree` : Effet d'activité, modélise la propension des nœuds ayant un grand nombre de liens sortants à en envoyer plus.
- `indegPop` : Popularité généralisée (propension croissante des nœuds populaires à attirer encore plus de liens).
- `outAct` : Activité généralisée (propension croissante des nœuds actifs à initier plus de liens).

### Effets structurels avancés

- `inertia` : Effet de mémoire ou persistance, pour modéliser la probabilité de maintien des liens d'une période à l'autre.
- `gwesp` : Effet de pondération géométrique pour la fermeture triadique (Generalized Weighted Edgewise Shared Partner), modèle la formation de triangles en tenant compte du nombre de partenaires partagés.
- `gwdegree` : Effet de degré géométrique généralisé, pour les réseaux ayant une distribution de degré spécifique.
- `isolates` : Probabilité pour un nœud de rester isolé, utile pour modéliser la structure d’isolement dans le réseau.

### Effets basés sur des attributs spécifiques (covariables)

- `totAltX` : Effet d’accumulation de covariable, additionne les attributs d’altér (par exemple, l’âge moyen des amis).
- `totSimX` : Similarité totale d’une covariable entre les paires connectées.
- `avAltX` : Moyenne des attributs d’altér, modélise l’influence de la moyenne des covariables sur le comportement de l’ego.
- `sameWX` : Effet d'homophilie sur une covariable continue, examine la similarité continue entre les nœuds.

### Effets comportementaux et influence

- `behavior` : Modèle de comportement, modélise l’évolution d'un comportement ou attribut mesuré sur une échelle continue.
- `behEgo` : Effet comportemental d'ego, représente l’influence d’un comportement spécifique de l’ego sur le réseau.
- `behAlt` : Effet comportemental d’altér, montre comment le comportement de l’alter affecte la probabilité de formation de liens.
- `totalBehDiff` : Différence totale de comportement entre les nœuds connectés, modélise la tolérance à la différence de comportement.

### Effets temporels

- `timeDummy` : Effet temporel, permet de modéliser les changements structurels du réseau au fil du temps en appliquant un coefficient distinct pour chaque période.
- `eval` : Effet d'évaluation temporelle, utile pour des modèles dynamiques où les comportements ou relations changent à chaque période.

### Autres effets

- `avSimX` : Moyenne de la similarité sur une covariable entre l’ego et les alters.
- `avDist2AltX` : Distance moyenne de l’ego par rapport à une variable exogène définie sur les alters.
- `popAlt` : Popularité basée sur les attributs des alters.
- `squaredOutdegree` : Effet de l’activité quadratique, modélise une dynamique de saturation pour l’initiation de nouveaux liens.
- `densityFixed` : Fixe la densité globale du réseau, utilisé pour des réseaux dont la taille est constante.

### Exemple d’utilisation avancée

Voici un exemple d'utilisation avancée pour modéliser un réseau de sites web impliqués dans une controverse. Ce modèle inclut des effets adaptés à un réseau de citations dans lequel chaque nœud est un site web. On utilise les covariables `typeactor` (type d’acteur, par exemple, institution, média, blogueur, etc.) et `politicsOpinion` (opinion politique). Ce modèle prend en compte la structure du réseau (activité, popularité), l'homophilie et la dynamique temporelle.

### Exemple d’utilisation avancée adapté à un réseau de citations de sites web

```r
# Inclusion des effets pour un réseau de sites web dans une controverse
effects <- includeEffects(effects, density)                        # Densité du réseau
effects <- includeEffects(effects, recip)                          # Réciprocité (rare, mais incluse pour détecter les liens bidirectionnels)
effects <- includeEffects(effects, transTrip)                      # Transitivité (clustering entre sites ayant des liens communs)
effects <- includeEffects(effects, sameX, interaction1="typeactor")  # Homophilie selon le type d’acteur
effects <- includeEffects(effects, sameX, interaction1="politicsOpinion")  # Homophilie par opinion politique

# Effets de popularité et d'activité spécifiques à un réseau de sites web
effects <- includeEffects(effects, indegree, interaction1="activity")  # Popularité en fonction de l’activité (nombre de liens entrants)
effects <- includeEffects(effects, outdegree, interaction1="activity") # Activité (nombre de liens sortants)
effects <- includeEffects(effects, indegPop)                          # Popularité croissante (nœuds populaires attirant davantage de liens)
effects <- includeEffects(effects, outAct)                            # Activité croissante (nœuds actifs initiant plus de liens)

# Effets spécifiques pour un réseau de controverses
effects <- includeEffects(effects, inertia)                           # Effet de mémoire pour les liens récurrents
effects <- includeEffects(effects, avAltX, interaction1="politicsOpinion")  # Moyenne des opinions politiques parmi les alters
effects <- includeEffects(effects, altX, interaction1="typeactor")    # Influence du type d’acteur des alters sur les liens

# Effets temporels pour modéliser les dynamiques dans une controverse en ligne
effects <- includeEffects(effects, eval, interaction1="time")         # Effet temporel pour capturer l’évolution des citations
effects <- includeTimeDummy(effects, "time", period=2)               # Effet temporel par période pour capturer des changements structuraux

# Effet de comportement et influence des opinions politiques dans le réseau
effects <- includeEffects(effects, behAlt, interaction1="politicsOpinion")  # Influence des opinions politiques des alters
effects <- includeEffects(effects, totalBehDiff, interaction1="politicsOpinion")  # Différence d'opinion politique entre les nœuds

# Exemple d'utilisation avancée pour les effets de clustering
effects <- includeEffects(effects, gwesp, parameter=0.5)             # Fermeture triadique pondérée pour des clusters denses
effects <- includeEffects(effects, isolates)                         # Probabilité pour un site d’être isolé (sans liens)

# Affichage des effets choisis pour vérification
print(effects)
```

### Explication des effets inclus :

- **Densité, réciprocité et transitivité** : Ces effets permettent de modéliser la structure de base du réseau, en vérifiant la densité générale, la présence de liens bidirectionnels (rare mais possible) et la tendance à former des triangles dans le réseau, un indicateur de clusters autour de certains thèmes ou opinions.
- **Homophilie** : Les effets `sameX` pour `typeactor` et `politicsOpinion` capturent la tendance des sites à se lier en fonction de caractéristiques similaires, soit par type d’acteur, soit par opinion politique.
- **Popularité et activité** : `indegree` et `outdegree` mesurent la popularité et l'activité en fonction du nombre de liens entrants et sortants, tandis que `indegPop` et `outAct` capturent une tendance cumulative, où les nœuds populaires et actifs continuent d'attirer ou de créer plus de liens.
- **Effets temporels** : Les effets `eval` et `timeDummy` capturent les dynamiques de citation sur plusieurs périodes, permettant de modéliser l'évolution des citations dans la controverse.
- **Influence des opinions** : Les effets `behAlt` et `totalBehDiff` permettent de modéliser l'influence des opinions politiques des sites sur les choix de citation, ainsi que l'impact de la différence d'opinion entre sites sur leur probabilité de se lier.
- **Fermeture triadique pondérée (GWESP)** : Cet effet modélise les clusters denses au sein du réseau, souvent présents dans des groupes de sites ayant des opinions ou intérêts communs.
- **Isolement** : `isolates` permet de modéliser la probabilité qu’un site reste isolé, un phénomène fréquent dans les controverses où certains acteurs peuvent être mis à l’écart.

Ce code permet de créer un modèle d’analyse qui reflète les spécificités des réseaux de controverses en ligne, incluant les effets structurels, comportementaux et temporels pertinents pour les réseaux de citations dans un contexte de polarisation d'opinions.
## 2.3. Modèle TERGM avec btergm

Dans ce code, nous supposons que chaque élément de la liste `networks` est un réseau pour une période donnée et contient déjà les attributs nécessaires (par exemple, "age" et "gender").

```r
# Charger les packages nécessaires
if (!requireNamespace("btergm", quietly = TRUE)) install.packages("btergm")
library(btergm)

# Spécification et estimation du modèle TERGM avec les effets désirés
model_tergm <- btergm(
    networks ~ edges + 
    mutual + 
    transitiveties + 
    nodeicov("age") + 
    nodematch("gender"),
    R = 1000,         # Nombre d'itérations bootstrap pour l'estimation
    parallel = "snow", # Utilisation de parallélisme pour l'estimation
    ncpus = 4          # Nombre de CPUs pour le calcul parallèle (ajuster selon votre machine)
)

# Affichage des résultats du modèle
summary(model_tergm)
```

### Diagnostic de l’Ajustement avec Goodness-of-Fit (gof)

Pour vérifier la qualité de l’ajustement du modèle, on utilise **gof** pour comparer les réseaux observés aux réseaux simulés sur plusieurs dimensions.

```r
# Calcul de la qualité de l'ajustement du modèle TERGM
gof_results <- gof(model_tergm, 
                   statistics = c("degree", "edgecount", "triad.census"),
                   nsim = 100)  # Nombre de simulations pour l'évaluation de l'ajustement

# Visualisation des résultats du diagnostic d'ajustement
plot(gof_results)
```

### Calcul et Interprétation des Odd Ratios

Pour une interprétation approfondie des effets du modèle, nous calculons les **odd ratios** pour chaque coefficient. Les odd ratios indiquent l'impact relatif de chaque effet sur la probabilité de formation de liens.

```r
# Calcul des odd ratios pour chaque paramètre estimé
odd_ratios <- exp(coef(model_tergm))
names(odd_ratios) <- names(coef(model_tergm))
print(odd_ratios)
```

### Résumé Interprétatif des Paramètres

1. **Edges** : Un paramètre négatif pour les arêtes (edges) indiquerait une faible densité de liens dans le réseau.
2. **Mutual** : Un odd ratio supérieur à 1 pour `mutual` signifie une forte tendance à la réciprocité.
3. **Transitiveties** : Si le coefficient est positif, cela indique une tendance accrue à former des triades, suggérant une cohésion du réseau.
4. **Nodeicov("age")** : Ce paramètre quantifie l'influence de l'âge sur la probabilité de lien. Un odd ratio > 1 indiquerait que les liens sont plus probables avec un âge similaire.
5. **Nodematch("gender")** : L’homophilie de genre est mesurée ici ; un odd ratio > 1 pour `gender` montre une tendance accrue aux liens entre individus du même genre.

Ce code utilise directement la liste `networks` pour estimer un modèle TERGM dynamique, adapté à des réseaux évoluant sur plusieurs périodes.

## Bibliographie

Block, P., & Burnett Heyes, S. (2022). Sharing the load : Contagion and tolerance of mood in social networks. _Emotion_, _22_(6), 1193‑1207. [https://doi.org/10.1037/emo0000952](https://doi.org/10.1037/emo0000952)

Block, P., Hollway, J., Stadtfeld, C., Koskinen, J., & Snijders, T. (2022). Circular specifications and “predicting” with information from the future : Errors in the empirical SAOM–TERGM comparison of Leifeld & Cranmer. _Network Science_, _10_(1), 3‑14. [https://doi.org/10.1017/nws.2022.6](https://doi.org/10.1017/nws.2022.6)

Block, P., Stadtfeld, C., & Snijders, T. A. B. (2019). Forms of Dependence : Comparing SAOMs and ERGMs From Basic Principles. _Sociological Methods & Research_, _48_(1), 202‑239. [https://doi.org/10.1177/0049124116672680](https://doi.org/10.1177/0049124116672680)

Bright, D., Koskinen, J. H., & Malm, A. E. (2019). Illicit Network Dynamics : The Formation and Evolution of a Drug Trafficking Network. _Journal of Quantitative Criminology_, _35_(2), 237‑258. [https://doi.org/10.1007/s10940-018-9379-8](https://doi.org/10.1007/s10940-018-9379-8)

Fritz, C. (s. d.). _Statistical Approaches to Dynamic Networks in Society_.

Hanneke, S., Fu, W., & Xing, E. P. (2010). Discrete temporal models of social networks. _Electronic Journal of Statistics_, _4_(none), 585‑605. [https://doi.org/10.1214/09-EJS548](https://doi.org/10.1214/09-EJS548)

Krivitsky, P. N., & Handcock, M. S. (2014). A Separable Model for Dynamic Networks. _Journal of the Royal Statistical Society Series B: Statistical Methodology_, _76_(1), 29‑46. [https://doi.org/10.1111/rssb.12014](https://doi.org/10.1111/rssb.12014)

Leifeld, P., & Cranmer, S. J. (2022). The stochastic actor-oriented model is a theory as much as it is a method and must be subject to theory tests. _Network Science_, _10_(1), 15‑19. [https://doi.org/10.1017/nws.2022.7](https://doi.org/10.1017/nws.2022.7)

Leifeld, P., Cranmer, S. J., & Desmarais, B. A. (2018). Temporal Exponential Random Graph Models with btergm : Estimation and Bootstrap Confidence Intervals. _Journal of Statistical Software_, _83_, 1‑36. [https://doi.org/10.18637/jss.v083.i06](https://doi.org/10.18637/jss.v083.i06)

Stadtfeld, C., & Block, P. (2017). Interactions, Actors, and Time : Dynamic Network Actor Models for Relational Events. _Sociological Science_, _4_, 318‑352. [https://doi.org/10.15195/v4.a14](https://doi.org/10.15195/v4.a14)

Stadtfeld, C., Hollway, J., & Block, P. (2017). Dynamic Network Actor Models : Investigating Coordination Ties through Time. _Sociological Methodology_, _47_(1), 1‑40. [https://doi.org/10.1177/0081175017709295](https://doi.org/10.1177/0081175017709295)
