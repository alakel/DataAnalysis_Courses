L'analyse des réseaux sociaux a considérablement évolué au-delà de la simple représentation des liens et des connexions entre individus. En sciences sociales, il est essentiel non seulement de décrire ces réseaux, mais aussi de comprendre les mécanismes sous-jacents qui influencent la formation et l'évolution de ces liens. Les **modèles de graphes aléatoires exponentiels** (ERGM) répondent à ce besoin en offrant un cadre statistique pour analyser les structures de réseaux de manière rigoureuse, en tenant compte des relations entre les nœuds ainsi que des attributs spécifiques de ces derniers.

Dans ce cours, nous aborderons les fondements et les développements des ERGM, également connus sous l’appellation de modèles p*. Ces modèles permettent d'explorer des configurations spécifiques (telles que la réciprocité ou la transitivité) et d’intégrer des caractéristiques des nœuds (comme l’âge ou le genre) pour examiner comment elles influencent les probabilités de formation de liens dans le réseau. Nous explorerons également des variantes avancées comme les **modèles p2**, qui introduisent des effets de covariables pour les réseaux dirigés, apportant ainsi une flexibilité accrue pour les réseaux complexes et les applications interdisciplinaires.

Les modèles ERGM et p2 permettent d'adresser des questions critiques en sciences sociales : Comment les individus se regroupent-ils en fonction de leurs similarités ? Quels sont les rôles structuraux joués par différents acteurs dans un réseau ? Quels sont les mécanismes qui favorisent la formation de liens ou l’apparition de sous-groupes dans une organisation ? Ce cours vise à familiariser les étudiants avec ces concepts tout en leur permettant d'appliquer ces modèles à des jeux de données concrets.

L’accent sera mis sur la mise en œuvre pratique des ERGM en utilisant R, à travers des packages spécialisés tels que `ergm` et `btergm`, pour conduire des analyses sur des réseaux sociaux fictifs et interpréter les résultats de manière critique. Les activités et discussions incluront une analyse des forces et des limites de ces modèles, offrant ainsi aux étudiants une compréhension approfondie des défis méthodologiques liés à la modélisation des réseaux sociaux.

Voici la synthèse de l'État de l'art et de la distinction des modèles p* et p2, ainsi que leurs contributions spécifiques à l'analyse statistique des réseaux.

## Partie 1 : État de l'Art en Modélisation Statistique des Réseaux – ERGM, Modèles p* et p2

Les **modèles de graphes aléatoires exponentiels** (ERGM) constituent une avancée majeure pour la modélisation des structures complexes des réseaux sociaux. Cette partie détaille les fondements, les évolutions et les spécificités des **modèles p*** et **p2**, deux familles d'ERGM conçues pour capturer des motifs relationnels, comme la réciprocité et la transitivité, et pour prendre en compte des attributs individuels dans des réseaux dirigés et non-dirigés. 

### 1.1 Fondements des ERGM et Introduction des Modèles p*

L'article de **Holland et Leinhardt (1981)**, "An Exponential Family of Probability Distributions for Directed Graphs," est fondamental dans le domaine de l'analyse des réseaux, particulièrement pour avoir introduit le cadre mathématique des **modèles de graphes aléatoires exponentiels** (ERGM). Ce modèle vise à capturer des motifs relationnels récurrents, comme la réciprocité, au sein des réseaux dirigés, en offrant une formulation statistique robuste. Examinons en détail les enjeux, les fondements mathématiques, ainsi que l’algorithme et ses applications dans les sciences sociales computationnelles.

L'un des objectifs centraux des auteurs est de dépasser les limitations des modèles de graphes aléatoires simples (par exemple, Erdős-Rényi) qui ne capturent pas la complexité des dépendances relationnelles dans les réseaux sociaux. Les **réseaux sociaux dirigés** contiennent souvent des dépendances structurelles, telles que la réciprocité et la transitivité, qui influencent la formation des liens. L'ERGM proposé par Holland et Leinhardt permet de modéliser ces dépendances en introduisant une **distribution de probabilité exponentielle** pour les liens dans les réseaux dirigés. Ce modèle est particulièrement adapté aux analyses où les relations sont hiérarchisées ou asymétriques (comme dans les réseaux académiques de citation ou les interactions professionnelles).

**Fondements Algorithmique des ERGM**

L'approche mathématique adoptée par Holland et Leinhardt repose sur les **distributions de la famille exponentielle**. Holland et Leinhardt définissent plusieurs **statistiques de réseau** pour capturer les motifs d'intérêt dans les réseaux dirigés. Par exemple, la statistique de réciprocité compte le nombre de liens mutuels (i.e., lorsque deux nœuds ont des liens dirigés l’un vers l’autre). D'autres statistiques, comme celles capturant la **transitivité** ou les **triangles**, sont également intégrées dans les développements ultérieurs des ERGM pour modéliser la probabilité de liens entre nœuds en fonction de leurs relations existantes.

Pour estimer les paramètres, Holland et Leinhardt ont initié l'utilisation de méthodes d’estimation qui ont ensuite évolué avec les développements de l'algorithme **Monte Carlo par chaînes de Markov (MCMC)**. Cet algorithme fonctionne en simulant des échantillons de réseaux qui respectent la structure spécifiée par les paramètres et en ajustant ces paramètres pour maximiser la vraisemblance du modèle par rapport aux données observées. L’estimation par MCMC a permis de rendre les ERGM praticables pour des réseaux de taille moyenne, en contournant le problème de la constante de normalisation intractable.

Les étapes principales de l’algorithme sont les suivantes :
1. **Initialisation des paramètres** : Un vecteur de paramètres initial est fixé pour \( \theta \).
2. **Génération de graphes** : Des graphes sont générés aléatoirement en fonction des paramètres initiaux et des statistiques du réseau.
3. **Ajustement des paramètres** : Les paramètres \( \theta \) sont ajustés en fonction des différences entre les statistiques observées et celles attendues sous le modèle.
4. **Convergence** : L'algorithme continue jusqu'à atteindre une convergence, c'est-à-dire lorsque les paramètres \( \theta \) maximisent la vraisemblance de la distribution observée.

Cette méthode a été cruciale pour rendre les ERGM applicables dans des analyses empiriques de réseaux sociaux, car elle permet d’estimer les paramètres de manière itérative et approchée.

**Application aux sciences sociales**

Les modèles proposés par Holland et Leinhardt ont ouvert de nombreuses possibilités dans l’analyse des réseaux dirigés, notamment pour :
- **Étudier la réciprocité** dans des réseaux d'interaction sociale : En modélisant la probabilité de liens réciproques, les ERGM peuvent identifier des tendances à la réciprocité au sein de réseaux denses, comme des réseaux de collaboration ou d'amitié.
- **Analyser la transitivité** et la formation de groupes : Les statistiques de réseau incluses dans les ERGM permettent de détecter les triades fermées, signalant des sous-groupes fortement connectés au sein du réseau.
- **Modéliser des réseaux hiérarchiques** : En intégrant des paramètres directionnels, les ERGM sont adaptés à des réseaux où les relations ont un sens, comme les réseaux académiques ou les réseaux de citations.

L'approche formelle introduite par Holland et Leinhardt continue d'être développée, notamment avec des extensions bayésiennes et des modèles multi-niveaux, pour répondre aux défis des réseaux sociaux actuels, qui incluent des dynamiques temporelles et des hiérarchies complexes.

### 1.2 Développement des ERGM et Limitations

Les modèles de graphes aléatoires exponentiels (ERGM) ont connu des avancées méthodologiques majeures grâce aux contributions de **Tom Snijders** et de son équipe, qui ont abordé les défis computationnels et théoriques des ERGM et introduit des innovations comme les modèles **p* et p2** pour les réseaux sociaux dirigés et les modèles dynamiques pour les réseaux évolutifs. Ce cours explore en détail l’évolution des ERGM, les fondements méthodologiques posés par Snijders et son équipe, et leurs applications aux réseaux sociaux. Snijders et son équipe ont apporté une contribution cruciale en introduisant des méthodes d’estimation basées sur les **algorithmes Monte Carlo par chaîne de Markov (MCMC)**, ce qui a permis de surmonter les problèmes de calcul des premiers ERGM. Les MCMC permettent de simuler des échantillons de réseaux qui respectent les dépendances structurelles observées dans les réseaux réels, facilitant ainsi l’estimation des paramètres de l’ERGM.

Les modèles **p***, ou p-star, ont été développés par **Frank et Strauss (1986)** comme une première formalisation des ERGM en tant que famille exponentielle de distributions. Cependant, c’est grâce aux travaux de Snijders et ses collaborateurs que les p* ont pris en compte des aspects plus complexes de la structure des réseaux, notamment par l’intégration des attributs des nœuds dans les calculs de probabilité. L’idée est d’inclure des **statistiques de configuration** (comme les triangles ou les chemins) ainsi que les attributs individuels des nœuds (par exemple, l’âge, le genre, le statut social) pour modéliser la probabilité de formation des liens dans le réseau.

Les innovations méthodologiques de Snijders dans les modèles p* incluent :
- **Modélisation de l’homophilie et de l’hétérophilie** : En incluant des attributs individuels, les modèles p* permettent de modéliser la probabilité de connexion entre des nœuds en fonction de leurs similarités ou différences d’attributs.
- **Mesure de la transitivité et de la réciprocité** : Les ERGM permettent de quantifier la tendance des nœuds à former des triades fermées ou des liens réciproques, ajoutant une dimension d’analyse des relations multiples.

Les **modèles p2**, proposés par **van Duijn, Snijders et Zijlstra (2004)**, représentent une avancée majeure pour l’étude des réseaux dirigés où les relations sont asymétriques, comme les réseaux de citation ou de collaboration hiérarchiques. Contrairement aux modèles p*, les modèles p2 incluent explicitement :
- **Effets de réciprocité et de popularité** : Ils modélisent non seulement la probabilité de liens mutuels entre deux nœuds, mais également la propension d’un nœud à attirer des liens entrants en fonction de sa popularité.
- **Effets de réputation et de hiérarchie** : Les p2 permettent de prendre en compte des structures hiérarchiques, rendant possible l’analyse de réseaux dirigés où les attributs des nœuds déterminent la direction des liens.

Les modèles p2 sont particulièrement pertinents dans les réseaux académiques et organisationnels, où les attributs comme le statut académique ou la fonction professionnelle influencent fortement la probabilité de formation de liens.

### 1.3 Avancées Récentes et Approches Bayésiennes

### 1.3 Avancées Récentes et Approches Bayésiennes des ERGM

Dans la poursuite des avancées méthodologiques pour les modèles de graphes aléatoires exponentiels (ERGM), les approches bayésiennes, introduites récemment par **Hunter et Handcock (2022)**, ont apporté des solutions innovantes pour répondre aux défis des réseaux de grande taille et denses, où les données peuvent être incomplètes ou bruitées. Ces modèles bayésiens offrent une flexibilité accrue en combinant la capacité de modélisation probabiliste des ERGM avec la robustesse et la souplesse des approches bayésiennes. En effet, ils permettent de quantifier l’incertitude, de mieux gérer les dépendances dans les réseaux complexes, et de fournir des estimations fiables même en présence de données incomplètes.

Les modèles ERGM classiques sont limités par la complexité computationnelle et les problèmes d’estimation qui se posent dans les réseaux de grande taille, où les dépendances entre les nœuds deviennent difficiles à gérer. En outre, l’inférence dans les ERGM est particulièrement sensible aux données manquantes et au bruit dans les relations observées, ce qui limite l’utilisation des ERGM classiques dans des réseaux denses ou des contextes empiriques avec des données imparfaites.

Les approches bayésiennes pour les ERGM répondent à ces limitations en intégrant :
1. **Des intervalles de crédibilité pour les paramètres** : Permettant de capturer l’incertitude des estimations et de fournir une évaluation plus nuancée de la probabilité de certaines configurations de liens.
2. **Une modélisation robuste pour les données manquantes** : Grâce aux méthodes d’imputation bayésienne, les ERGM bayésiens gèrent mieux les absences de données, offrant des prédictions plus stables.
3. **Une intégration efficace des données bruitées** : Les modèles bayésiens ajustent les estimations en fonction de la variabilité et de l’incertitude des données, rendant ces modèles plus adaptés aux réseaux sociaux denses et aux interactions en ligne, souvent perturbés par des erreurs de mesure.

Ces apports permettent ainsi une analyse plus approfondie des configurations de réseau, comme la réciprocité, la transitivité et les motifs relationnels complexes, même dans des environnements de données imparfaits. 

La spécification bayésienne des ERGM repose sur l’estimation des paramètres en utilisant une distribution a priori, qui reflète les croyances initiales sur les valeurs probables des paramètres avant d'observer les données. Les paramètres des motifs relationnels (tels que la réciprocité, les triangles, etc.) sont ensuite ajustés en fonction des données observées, via des **algorithmes d'échantillonnage MCMC** ou d'autres méthodes d’échantillonnage stochastique, comme l’échantillonnage de Gibbs.

Les ERGM bayésiens sont particulièrement adaptés aux réseaux complexes, où les méthodes classiques peuvent échouer ou fournir des résultats biaisés. Leur utilisation est courante dans les domaines suivants :
1. **Réseaux de recherche et réseaux académiques** : Dans ces réseaux, les liens peuvent être influencés par des attributs professionnels ou thématiques (domaines de recherche, institution d’appartenance) et sont souvent partiellement observés. Les ERGM bayésiens permettent de gérer les absences de données.
2. **Réseaux en ligne et réseaux sociaux** : Les réseaux d’interaction en ligne, tels que Twitter ou Facebook, contiennent des liens peu stables et souvent sujets à du bruit de mesure. Les ERGM bayésiens offrent une robustesse accrue pour l’analyse de ces structures.
3. **Réseaux organisationnels** : Dans les réseaux de collaboration ou de conseil au sein des organisations, où les informations sont parfois incomplètes ou cachées, les ERGM bayésiens fournissent des estimations plus fiables, permettant d’étudier les liens stratégiques.

Bien que les ERGM bayésiens soient une avancée majeure, leur application reste limitée par des défis computationnels :
- **Exigences en puissance de calcul** : Les calculs bayésiens nécessitent une infrastructure de calcul performante, surtout pour les réseaux massifs.
- **Convergence des algorithmes MCMC** : La convergence peut être lente, notamment dans les réseaux avec des structures complexes ou des motifs de dépendance nombreux.
- **Paramétrisation complexe** : La sélection des a priori et des distributions conditionnelles dans les ERGM bayésiens requiert une expertise avancée pour éviter des biais et garantir des résultats fiables.

### Références
- Brailly, J., & Viallet-Thevenin, S. (2014). Exponential Random Graph Models for Social Networks: Theory, Methods, and Applications. *Bulletin de Méthodologie Sociologique*, 123, 80-87【347†source】.
- Cranmer, S. J., & Desmarais, B. A. (2011). Inferential Network Analysis with Exponential Random Graph Models. *Political Analysis*, 19(1), 66-86【346†source】.
- van Duijn, M. A., Snijders, T. A., & Zijlstra, B. J. (2004). p2: A random effects model with covariates for directed graphs. *Social Networks*, 26(3), 249-280.

## Partie 2 : Mise en Œuvre en R - Application des ERGM et des Modèles Bayesien ERGM

Dans cette section, nous allons implémenter les modèles ERGM classiques et ERGM bayésiens pour explorer des configurations complexes dans des réseaux. Ces exemples seront opérationnels pour des réseaux orientés et non-orientés, intégrant des attributs de nœuds, de la réciprocité, et de la transitivité. Avant de commencer, nous allons installer et charger les packages nécessaires (`ergm` pour les ERGM classiques et `Bergm` pour l’estimation bayésienne).

```r
# Installer les packages si nécessaire
install.packages("ergm")
install.packages("Bergm")
install.packages("network")

# Charger les packages
library(ergm)
library(Bergm)
library(network)
```

### 2.1 Modélisation avec ERGM Classique

Nous allons maintenant construire un modèle ERGM pour capturer des effets de base comme la densité (via le terme `edges`), la réciprocité (`mutual`), et les effets d’homophilie et d’activité en fonction des attributs des nœuds (`activity_level` et `popularity`).

```r
# Estimation de l'ERGM avec des termes de réciprocité, d'activité et de popularité
model_ergm <- ergm(network ~ edges + mutual + triangle + nodematch("activity_level") + nodeicov("popularity") + nodeocov("activity_level"))

# Résumé du modèle
summary(model_ergm)
```

**Interprétation des Termes**
- **`edges`** : Estime la probabilité de formation de liens dans le réseau.
- **`mutual`** : Modélise la réciprocité, capturant la tendance des liens à être mutuels.
- **`triangle`** : Représente la transitivité dans le réseau, indiquant une tendance des nœuds connectés à partager des liens avec des tiers communs.
- **`nodematch("activity_level")`** : Modélise l’homophilie, indiquant si les nœuds avec des niveaux d’activité similaires ont une probabilité plus élevée de se connecter.
- **`nodeicov("popularity")`** et **`nodeocov("activity_level")`** : Capturent les effets d’activité et de popularité directionnels.
### 2.2 Modélisation ERGM Bayésienne avec `Bergm`

Les modèles ERGM bayésiens, disponibles dans le package `Bergm`, fournissent une approche alternative pour estimer les paramètres du modèle en prenant en compte l'incertitude inhérente et les intervalles de crédibilité. Nous utiliserons ici le même réseau pour estimer les paramètres bayésiens.

```r
# Modèle ERGM Bayésien
model_bergm <- bergm(network ~ edges + mutual + triangle + nodematch("activity_level") +
                     nodeicov("popularity") + nodeocov("activity_level"))

# Résumé des résultats bayésiens
summary(model_bergm)
plot(model_bergm)
```


**Comparaison entre ERGM Classique et ERGM Bayésien**

- **ERGM Classique** : Fournit des estimations précises mais peut être limité pour des réseaux très denses ou incomplets. Il nécessite des méthodes de diagnostic pour confirmer la validité des modèles.
- **ERGM Bayésien** : Permet une approche plus flexible et robuste, surtout pour des réseaux de grande taille ou partiellement observés. Cependant, les modèles bayésiens peuvent être plus coûteux en termes de temps de calcul.

**Avantages des ERGM Bayésiens**
- **Incertitude et crédibilité** : Les paramètres incluent des intervalles de crédibilité, permettant de mieux quantifier l'incertitude.
- **Adaptation aux données manquantes** : Les ERGM bayésiens sont plus flexibles face aux réseaux incomplets, un atout pour les réseaux sociaux complexes.


### 2.3 Modèles avancées appliqués aux réseaux de citations

#### Modèle Avancé d'un réseau de citation

```r
# Modèle intégrant les effets de prestige académique
citation_model <- ergm(net ~ edges + mutual
                       nodematch("field") +
                       nodefactor("institution") +
                       nodeicov("impact_factor") +    # Effet de l'impact factor
                       nodeocov("publication_year") + # Effet temporel
                       gwdegree(0.3, fixed=TRUE) +    # Distribution des degrés
                       gwesp(0.2, fixed=TRUE) +       # Clustering pondéré
                       cycle(3) +                     # Citations cycliques dans les controverse intense type twitter
                       twopath +
                       degree(2) +                    # Citations intermédiaires
                       esp(0:3) +                     # Chemins de citation courts
                       dsp(0:3),                      # Chemins de citation dirigés
                       control = control.ergm(MCMC.burnin = 30000,
                                              MCMC.samplesize = 10000,
                                              MCMLE.maxit=20,
                                              parallel = 4,
                                              parallel.type="PSOCK"),
                       constraints = ~ bd(maxout = 350, minout = 1))

```
Le code représente un modèle ERGM (Exponential Random Graph Model) utilisé pour analyser les réseaux de citations académiques. Voici une explication détaillée de chaque paramètre et des options possibles.

**Paramètres de Modélisation des Effets dans le Modèle ERGM**

Effets de réseau
1. **edges** : Ce paramètre modélise la présence d’un lien dans le réseau. Chaque lien contribue de manière additive au modèle. `edges` est toujours inclus pour prendre en compte la probabilité de base d'un lien dans le réseau.
2. **triangle** : Représente la tendance des liens à former des triangles, capturant l'effet de clustering local.
3. **mutual** : Modélise la réciprocité dans les liens, soit lorsque deux nœuds se citent mutuellement.
4. **transitiveties** : Ajoute l’effet de transitivité, où si `A cite B` et `B cite C`, il y a une probabilité accrue que `A cite C`.
5. **nodematch("field")** : Modélise la propension à la citation entre les auteurs appartenant au même domaine (`field`). Effet d'homophilie. `nodematch` est pertinent lorsque l’on souhaite évaluer les liens préférentiels entre nœuds de mêmes catégories (par exemple, liens entre pages de même type, personnes ayant le même genre ou la même institution).

Effet d'attributs
6. **nodefactor("institution")** : Tient compte de l'effet d’appartenance institutionnelle sur les citations. Si on utilise `nodefactor("institution")` dans un réseau académique, le modèle va mesurer l’effet de chaque institution spécifique sur la probabilité de recevoir des citations ou de former des liens, capturant ainsi si certaines institutions sont plus centrales que d’autres dans le réseau.
7. **nodeicov("impact_factor")** : Effet de l’impact factor de chaque publication. `nodeicov` signifie que cette covariable est prise en compte comme une caractéristique d’importance des nœuds à recevoir des noeuds. C'est une fonction spécifique de 'nodecov'
8. **nodeocov("publication_year")** : Effet temporel sur les citations, `nodeocov` prenant en compte une covariable pour la création de liens.

Effet des réseaux spécifiques type invariant d'échelle
9. **gwdegree(0.3, fixed=TRUE)** : Ce paramètre, appelé "Geometrically Weighted Degree" (degré pondéré géométriquement), modélise la distribution des degrés. Ici, `0.5` contrôle l'inclinaison (ou la pondération).
    - **Valeur de pondération** : La valeur `0.5` peut être ajustée pour des distributions de degré plus ou moins concentrées.
    - **fixed** : Lorsque `fixed=TRUE`, la valeur de pondération est maintenue constante.
10. **gwesp(0.8, fixed=TRUE)** : Ce paramètre, "Geometrically Weighted Edgewise Shared Partner" (partenariat pondéré géométriquement), capture le degré de clustering (ou fermeture des triangles). La pondération `0.5` contrôle l’effet d’échelle.
	- **Valeur de pondération** : `0.5` peut être modifié pour augmenter ou diminuer le niveau de clustering souhaité.

11. **cycle(3)** : Prend en compte les cycles de longueur 3 dans le réseau, modélisant les citations cycliques.
    - **Longueur du cycle** : La valeur `3` peut être ajustée (par exemple, `cycle(4)`) pour étudier des cycles plus longs.
12. **twopath** : Mesure la présence de chemins de longueur 2 (indirects), indiquant des structures de médiation dans les citations.
    - **Valeurs** : Non paramétrable directement, utilisé pour capturer les chemins indirects dans le modèle.
13. **degree(2)** : Contribue à l’effet de centralité, en spécifiant les nœuds ayant au moins 2 liens entrants ou sortants.
    - **Valeurs** : La valeur `2` peut être augmentée ou diminuée pour capturer différents niveaux de centralité.
14. **esp(0:3)** : Modèle les "Edgewise Shared Partners" (partenaires partagés en arêtes) pour des chemins de citation courts.
    - **Intervalle des valeurs** : `0:3` signifie qu’on prend en compte les chemins courts entre 0 et 3. Cet intervalle peut être ajusté selon les distances de citation d’intérêt.
15. **dsp(0:3)** : Modèle les "Directed Shared Partners" (partenaires partagés dirigés), pour des chemins dirigés de 0 à 3.
    - **Intervalle des valeurs** : Ajustable, comme `esp`, selon les spécificités du réseau.

**Paramètres de Contrôle de l’ERGM**

Les paramètres de contrôle définissent les spécifications du processus de simulation pour l’ERGM :

1. **MCMC.burnin = 60000** : Nombre de premières étapes de la simulation à ignorer (pour éviter le biais initial).
    - **Valeur** : Peut être augmenté si la convergence n'est pas atteinte, par exemple, `100000`.
2. **MCMC.samplesize = 30000** : Taille de l’échantillon après la phase de burn-in.
    - **Valeur** : Augmenter cette taille peut améliorer la précision, mais allonge le temps de calcul.
3. **MCMLE.maxit = 25** : Nombre maximal d’itérations pour l’algorithme MCMLE (Monte Carlo Maximum Likelihood Estimation).
    - **Valeur** : À ajuster en fonction de la complexité du modèle. Une valeur plus élevée peut être nécessaire pour des réseaux très denses.
4. **parallel = 4** : Spécifie le nombre de cœurs utilisés pour le calcul parallèle.
    - **Valeur** : Le nombre de cœurs peut être augmenté ou diminué selon la capacité de l’ordinateur.
5. **parallel.type = "PSOCK"** : Type de cluster parallèle à utiliser, ici "PSOCK" (type de cluster flexible en R).
    - **Valeurs** : Peut être `MPI` pour un environnement plus performant, si disponible.

**Contrainte de Degré**

1. **constraints = ~ bd(maxout = 100, minout = 1)** : Contrainte de degré spécifiant les limites des liens sortants.
    - **maxout** : Limite supérieure des liens sortants d’un nœud. Ici, `100` pour éviter les nœuds trop centraux.
    - **minout** : Nombre minimum de liens sortants d’un nœud, ici `1`. 
    - **`maxin`** : Limite maximale pour les liens **entrants** d’un nœud. Cela contrôle le nombre maximal de connexions que le nœud peut recevoir.
    - **`minin`** : Limite minimale pour les liens **entrants** d’un nœud, garantissant qu’un nœud a au moins un certain nombre de connexions entrantes.

Ce modèle avancé capture les effets de prestige, centralité, clustering et structures de citation dans les réseaux académiques, offrant une modélisation riche des dynamiques de citation.

#### Approche Bayésienne pour Réseaux de Citations

```r
# Chargement de BERGM et configuration du modèle bayésien
library(BERGM)

# Modèle bayésien équivalent à l'ERGM
citation_model_bergm <- bergm(
  net ~ edges + mutual +
    nodematch("field") +
    nodefactor("institution") +
    nodeicov("impact_factor") +    # Effet de l'impact factor
    nodeocov("publication_year") + # Effet temporel
    gwdegree(0.3, fixed=TRUE) +    # Distribution des degrés
    gwesp(0.2, fixed=TRUE) +       # Clustering pondéré
    cycle(3) +                     # Citations cycliques
    twopath +
    degree(2) +                    # Citations intermédiaires
    esp(0:3) +                     # Chemins de citation courts
    dsp(0:3),                      # Chemins de citation dirigés
  
  # Paramètres MCMC pour BERGM
  iterations = 30000,              # Nombre total d'itérations pour assurer convergence
  burn.in = 5000,                  # Phase de burn-in pour stabiliser l'échantillon
  thinning = 10,                   # Intervalle de thining pour réduire la corrélation
  gamma = 0.5                      # Précision de l’échantillonnage MCMC
)

```


**Explication des Paramètres pour BERGM**

- **`iterations = 30000`** : Détermine le nombre total d'itérations pour l’échantillonnage MCMC. Ici, nous augmentons le nombre pour garantir une exploration adéquate du modèle.
    
- **`burn.in = 5000`** : Nombre d'itérations initiales à ignorer pour stabiliser l'échantillon. Un burn-in de 5000 assure que seules les valeurs stabilisées sont conservées.
    
- **`thinning = 10`** : Chaque 10e itération est conservée pour réduire la corrélation entre les échantillons consécutifs, améliorant ainsi l'indépendance de l'échantillonnage.
    
- **`gamma = 0.5`** : Précision de l’échantillonnage MCMC. Un gamma inférieur à 1 ralentit la progression de l’échantillonnage, assurant une exploration plus précise des paramètres.
    

Points à Considérer pour la Conversion

- **Absence de `bd`** : Les contraintes de degré (minout et maxout) ne sont pas strictement possibles en `BERGM`. Un post-traitement peut être réalisé pour exclure les nœuds qui dépassent ces limites.
    
- **Différences dans la gestion des paramètres de contrôle** : `BERGM` limite la personnalisation du processus MCMC. Les paramètres de `control.ergm` dans `ERGM` doivent être approximés avec `iterations`, `burn.in`, et `thinning`.

### 2.4 Validation et interprétation des modèles

```r
#### Diagnostic et Validation Spécifique aux Citations

# Fonction de diagnostic personnalisée pour ERGM et BERGM
citation_diagnostics <- function(model, model_type = "ergm", statist = c("degree", "espartners", "dspartners", "triadcensus") ) {
  # MCMC diagnostics
  mcmc.diagnostics(model)
  
  # Goodness of fit spécifique aux réseaux de citation
  if (model_type == "ergm") {
    gof_stats <- gof(model, 
                     statistics=statist,
                     control = control.gof.ergm(nsim = 50))
  } else if (model_type == "bergm") {
    gof_stats <- gof(model, 
                     statistics=statist,
                     control = control.gof.bergm(nsim = 50))
  }
  
  plot(gof_stats)
  return(gof_stats)
}

# Exécution des diagnostics
ergm_diagnostics <- citation_diagnostics(net, "ergm") # bergm_diagnostics <- citation_diagnostics(net, "bergm")

#### Interprétation des Résultats pour Réseaux de Citations

# Extraction et analyse des coefficients pour ERGM
summary(net)

# Calcul des odds ratios pour les effets significatifs (ERGM)
odds_ratios_ergm <- exp(coef(net))

# Analyse des effets de prestige
summary(net)$coefficients

## Visualisation et Interprétation

# Fonction de visualisation des résultats
plot_citation_results <- function(model) {
  # Tracé des distributions postérieures
  par(mfrow=c(2,2))
  plot(model, 
       main=c("Impact Factor Effect",
              "H-index Effect",
              "Field Homophily",
              "Base Edge Effect"))
  
  # Création d'un réseau prédit
  sim_net <- simulate(model, nsim = 5)
  plot(sim_net, 
       vertex.col=V(net)$field,
       edge.arrow.size=0.5,
       main="Simulated Citation Network")
}

plot_citation_results(net)

# Comparaison des paramètres des réseaux simulés avec le réel A REVOIR avec la fonction TABLEAUX de caracteristiques
# Fonction améliorée de comparaison des réseaux en utilisant compute_network_parameters
compare_networks <- function(original_net, simulated_nets) {
  # Calcul des statistiques pour le réseau original
  original_stats <- compute_network_parameters("Original", nodes = V(original_net), links = E(original_net))
  
  # Calcul des statistiques pour chaque réseau simulé
  sim_stats_list <- lapply(1:length(simulated_nets), function(i) {
    compute_network_parameters(paste("Simulated", i), nodes = V(simulated_nets[[i]]), links = E(simulated_nets[[i]]))
  })
  
  # Fusionner les résultats des simulations dans un seul DataFrame
  sim_stats_df <- do.call(rbind, sim_stats_list)
  
  # Calculer la moyenne des statistiques des réseaux simulés
  mean_sim_stats <- data.frame(t(colMeans(sim_stats_df[, -1])))  # Moyenne des colonnes sauf le nom
  mean_sim_stats$Name <- "Simulated_Mean"
  
  # Combiner le réseau original, les simulations et la moyenne des simulations dans un DataFrame final
  comparison_df <- rbind(original_stats, sim_stats_df, mean_sim_stats)
  
  # Afficher les résultats
  print("Statistiques de comparaison des réseaux :")
  print(comparison_df)
  
  # Tracer les comparaisons pour quelques statistiques clés
  par(mfrow = c(1, 3))
  barplot(c(original_stats$Density, mean_sim_stats$Density), 
          beside = TRUE, col = c("blue", "red"),
          main = "Density Comparison",
          names.arg = c("Original", "Simulated Mean"),
          ylab = "Density")
  legend("topright", legend = c("Original", "Simulated Mean"), fill = c("blue", "red"))
  
  barplot(c(original_stats$Mean_Degree, mean_sim_stats$Mean_Degree),
          beside = TRUE, col = c("blue", "red"),
          main = "Mean Degree Comparison",
          names.arg = c("Original", "Simulated Mean"),
          ylab = "Mean Degree")
  legend("topright", legend = c("Original", "Simulated Mean"), fill = c("blue", "red"))
  
  barplot(c(original_stats$Clustering, mean_sim_stats$Clustering),
          beside = TRUE, col = c("blue", "red"),
          main = "Clustering Comparison",
          names.arg = c("Original", "Simulated Mean"),
          ylab = "Clustering Coefficient")
  legend("topright", legend = c("Original", "Simulated Mean"), fill = c("blue", "red"))
  
  return(comparison_df)
}

# Exécution de la comparaison
sim_networks <- simulate(model, nsim = 5)
comparison_df <- compare_networks(net, sim_networks)

```

# Partie 3 : Applications des ERGM en Sciences Sociales

Les **modèles de graphes aléatoires exponentiels (ERGM)** et les **modèles p2** ont apporté des perspectives novatrices dans l’analyse des réseaux sociaux. En permettant d’intégrer des caractéristiques individuelles et des mécanismes relationnels, ces modèles offrent une compréhension détaillée de la structuration des réseaux sociaux et de la dynamique des interactions entre les acteurs. Voici des exemples de recherches appliquant ces modèles dans des contextes variés, illustrant la portée analytique et sociologique des ERGM et des modèles p2.

## 3.1. Études d'Amitié et d'Homophilie dans les Écoles

**Contexte et Objectifs**
Les réseaux d'amitié entre adolescents sont un domaine privilégié pour appliquer les ERGM, permettant d’examiner comment des caractéristiques individuelles, comme le genre, l’ethnicité ou le statut socio-économique, influencent la formation de liens amicaux. **Goodreau, Kitts et Morris (2009)** ont utilisé les ERGM pour explorer les tendances d'homophilie dans des réseaux scolaires, en particulier comment les élèves forment des liens avec ceux qui leur ressemblent.

**Méthodologie et Mise en Œuvre**
Les auteurs ont modélisé des réseaux d'amitié en intégrant des termes pour la **transitivité** (les amis d'un ami tendent à être amis) et l'**homophilie** (les élèves ayant des caractéristiques similaires, comme le même genre ou la même ethnie, sont plus susceptibles de devenir amis). Dans cet exemple, un **modèle ERGM** avec des paramètres pour l'homophilie (ex. `nodematch("gender")`), la réciprocité et les triangles a été estimé pour tester si les caractéristiques individuelles augmentent les chances de formation de liens.

**Résultats et Interprétation**
Les résultats montrent que les élèves forment des groupes selon leurs caractéristiques similaires (homophilie de genre et d’ethnicité), et ces groupes se structurent en sous-groupes denses via la transitivité. Ce phénomène indique une **polarisation sociale** dans les réseaux d'amitié scolaires, où les élèves se regroupent avec leurs semblables, ce qui peut avoir des implications importantes en termes de ségrégation sociale dès le plus jeune âge.

## 3.2. Analyse des Réseaux de Collaboration Académique

**Contexte et Objectifs**
Les réseaux de collaboration académique, basés sur les co-publications entre chercheurs, révèlent des dynamiques de soutien et de coopération au sein des disciplines scientifiques. **Lomi et Pattison (2006)** ont analysé ces réseaux en intégrant des effets de statut, de discipline, et de proximité institutionnelle. Cette approche visait à comprendre comment les caractéristiques des chercheurs influencent la probabilité de former des collaborations, avec des implications pour la diffusion des connaissances.

**Méthodologie et Mise en Œuvre**
Les ERGM ont été appliqués pour modéliser la formation des liens de co-publication, avec des termes pour la **transitivité** (collaborations triangulaires entre chercheurs), et des termes de **nodematch** pour représenter l'homophilie disciplinaire (ex. nodematch("discipline")). Les chercheurs dans la même institution ou avec des intérêts disciplinaires communs avaient une probabilité plus élevée de collaborer.

**Résultats et Interprétation**
L'étude révèle une forte tendance à l'homophilie dans les collaborations, les chercheurs ayant tendance à travailler avec ceux qui partagent leurs intérêts disciplinaires et statut institutionnel. Ce résultat souligne l’importance des similarités académiques dans les réseaux de co-publication, avec une tendance à la formation de sous-groupes disciplinaires au sein des réseaux scientifiques, ce qui favorise l'émergence de « silos » académiques.

## 3.3. Études des Réseaux Criminels et Identification des Rôles

**Contexte et Objectifs**
L'analyse des réseaux criminels vise à identifier des rôles spécifiques au sein de groupes criminels, tels que les **leaders**, les **facilitateurs**, et les **exécuteurs**. Les ERGM sont utilisés pour modéliser les interactions entre ces membres en fonction de leur position et de leur influence au sein du réseau criminel. **Bright et Hughes (2012)** ont appliqué les ERGM pour détecter les rôles organisationnels dans des réseaux de crime organisé.

**Méthodologie et Mise en Œuvre**
Les modèles ERGM dans ce contexte incluent des termes de **triangle** pour capturer des sous-groupes de coopération triangulaire entre membres du réseau, des termes de **degré** pour analyser la centralité (ex. `degree` pour les leaders) et des termes de **nodematch** pour évaluer si certains rôles spécifiques (comme facilitateurs et exécuteurs) tendent à interagir.

**Résultats et Interprétation**
Les résultats montrent une structure de sous-groupes denses autour de certains membres centraux, qui apparaissent comme des **leaders** ou **facilitateurs** dans le réseau. Cette organisation en sous-groupes, avec des rôles spécifiques bien définis, met en évidence des **formes de collaboration hiérarchique** dans les réseaux criminels. Ces analyses sont utiles pour les autorités, en particulier pour comprendre comment les organisations criminelles maintiennent leur stabilité et leur résilience.

## 3.4. Réseaux de Soutien Social en Santé Publique

**Contexte et Objectifs**
Les réseaux de soutien social jouent un rôle crucial dans la santé publique, notamment pour la **prévention et la diffusion d’informations** en matière de santé. **Goodreau et Morris (2009)** ont appliqué des ERGM pour analyser comment les individus forment des liens de soutien en fonction de leurs besoins en matière de santé et de soutien social.

**Méthodologie et Mise en Œuvre**
Les ERGM ont été utilisés pour modéliser les connexions dans les réseaux de soutien, en intégrant des termes de **nodematch** pour tester les effets de similarité (ex. nodematch("besoins_de_santé")). Les termes de **degré** et **mutualité** ont été ajoutés pour tester si les individus sont plus susceptibles de se connecter à ceux avec un besoin similaire ou complémentaire de soutien.

**Résultats et Interprétation**
Les résultats montrent que les individus forment des liens en fonction de leurs besoins similaires ou complémentaires en matière de santé, créant des sous-groupes de soutien. Cette étude révèle que l’homophilie de besoins est un facteur clé de structuration dans les réseaux de soutien social, soulignant l’importance des liens entre pairs pour la prévention et le soutien en santé publique.

## **3.5. Réseaux Politiques et Alliances Internationales**

**Contexte et Objectifs**
Les ERGM ont été appliqués à l'analyse des **alliances internationales**, pour comprendre comment les pays forment des coalitions en fonction de leurs attributs et des alliances existantes. **Cranmer et Desmarais (2011)** ont utilisé les ERGM pour explorer les dynamiques des alliances politiques internationales, en prenant en compte les attributs des pays et les structures locales d’alliance.

**Méthodologie et Mise en Œuvre**
Les ERGM incluent des termes pour la **réciprocité** (alliances bilatérales), et des termes de **triangle** pour capturer les alliances triangulaires. Les termes de **nodematch** ont été utilisés pour tester l’influence des attributs des pays (comme l'orientation politique ou économique) sur la formation des alliances.

**Résultats et Interprétation**
Les résultats montrent que les pays ont tendance à former des alliances avec des partenaires partageant des caractéristiques similaires, en particulier en termes d'orientation politique. Les configurations triangulaires observées montrent que les alliances internationales fonctionnent souvent en réseaux denses, avec des coalitions interconnectées, renforçant les relations entre alliés de longue date.

Ces exemples illustrent la grande variété des applications des ERGM et des modèles p2 en sciences sociales. Chaque étude montre comment les réseaux sociaux se forment et évoluent en fonction de caractéristiques individuelles et de mécanismes de structuration relationnelle. Ces méthodes apportent ainsi des outils puissants pour analyser les dynamiques sociales, qu’il s’agisse d’amitiés, de collaborations, de soutien ou d’alliances internationales, contribuant à une compréhension plus fine de la complexité des relations humaines.

### Références

- - **Bright, D., & Hughes, S. (2012)**. Criminal network analysis and visualisation: Investigating relational data for criminal intelligence purposes using exponential random graph models. _Journal of Criminal Justice_, 40(1), 43-55.

- **Cranmer, S. J., & Desmarais, B. A. (2011)**. Inferential network analysis with exponential random graph models. _Political Analysis_, 19(1), 66-86.

- **Goodreau, S. M., Kitts, J. A., & Morris, M. (2009)**. Birds of a Feather, Or Friend of a Friend? Using Exponential Random Graph Models to Investigate Adolescent Social Networks. _Demography_, 46(1), 103-125.

- **Lomi, A., & Pattison, P. E. (2006)**. Manufacturing relations: An empirical study of the organizational foundations of network structure. _Social Networks_, 28(4), 349-367.

- **Papachristos, A. V., Braga, A. A., & Hureau, D. M. (2013)**. Social networks and the risk of gunshot injury. _Journal of Urban Health_, 90(5), 992-1003.

- **Robins, G. L., Pattison, P., & Wang, P. (2009)**. Closure, connectivity and degree distributions: Exponential random graph (p*) models for directed social networks. _Social Networks_, 31(2), 105-117.
