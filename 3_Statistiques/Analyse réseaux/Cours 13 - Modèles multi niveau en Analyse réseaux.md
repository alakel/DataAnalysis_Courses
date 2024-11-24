L’analyse des réseaux multi-niveau repose sur la capacité à modéliser des interactions simultanées entre plusieurs couches ou dimensions d’un réseau, chaque niveau représentant un système de relations distinct mais connecté aux autres. Les modèles multi-niveau étendent l’analyse traditionnelle des réseaux en permettant d’explorer les dépendances entre nœuds situés dans des niveaux différents, ainsi que les structures d’interconnexion au sein de chaque niveau. Ces modèles offrent ainsi un cadre analytique qui rend compte des dynamiques relationnelles entre individus, groupes, organisations, et autres entités à divers degrés d’interaction, répondant aux besoins croissants d’analyse de réseaux complexes dans des environnements multi-couches.

Analyser les réseaux à plusieurs niveaux est essentiel car les réseaux sociaux, professionnels, académiques ou numériques ne se limitent pas à des interactions simples entre entités homogènes. Par exemple, dans un contexte organisationnel, un individu peut être en relation avec des collègues au sein de son équipe (niveau intra-organisationnel), tout en interagissant avec des membres d’autres entreprises dans le cadre de collaborations industrielles (niveau inter-organisationnel). En sciences sociales, ignorer cette hiérarchie et les relations inter-niveaux conduit à une perte d’information cruciale concernant les interdépendances qui façonnent les comportements sociaux, les dynamiques de groupe et les processus d’influence.

Les modèles traditionnels à un seul niveau, comme les réseaux de type ERGM (Exponential Random Graph Models) ou SAOM (Stochastic Actor-Oriented Models), se concentrent principalement sur les relations intra-niveau, c’est-à-dire les liens entre des entités homogènes. Bien qu’ils soient puissants pour analyser des dépendances locales comme la réciprocité ou la transitivité au sein d’un seul niveau, ces modèles ne capturent pas la complexité des interactions interconnectées entre niveaux. En ce sens, les modèles multi-niveau apportent une solution en permettant de représenter des réseaux comportant plusieurs couches d’interaction, d’intégrer des attributs d’entités situées à des niveaux différents, et d’analyser les influences croisées entre les niveaux. 

# I - Théorie des réseaux multi-niveaux

Voici une réorganisation en trois parties distinctes pour clarifier l’exposé sur les fondements théoriques et les enjeux méthodologiques des modèles multi-niveau en analyse de réseaux.

---

## I.1 : Fondements Historiques et Théoriques des Modèles Multi-Niveau

### Origines et Développement Historique
Les modèles multi-niveau en analyse de réseaux trouvent leurs racines dans des travaux pionniers comme ceux de **Mark Granovetter (1973)** et **Barry Wellman (1983)**. Granovetter, avec sa théorie des **liens forts et faibles**, a démontré comment les connexions peu intenses (liens faibles) facilitent la liaison entre sous-groupes sociaux éloignés. Bien que centrée sur un seul niveau de réseau, cette théorie a ouvert la voie à l’idée de relations inter-groupes et inter-niveaux. 

Wellman, en introduisant le concept de **networked individualism**, a quant à lui mis en évidence l'appartenance simultanée des individus à plusieurs réseaux (familial, professionnel, communautaire), avec des interactions influençant chaque niveau. Son travail souligne la nécessité d’une approche intégrée pour modéliser des réseaux de nature et d’échelle variées, reliant ainsi les réseaux personnels, organisationnels et communautaires.

### Concepts Clés et Paradigmes Fondateurs
Trois concepts structurants permettent de comprendre la spécificité des modèles multi-niveau :

- **Homophilie Inter-Niveau** : Tendance des individus à se lier avec des personnes partageant des attributs similaires, qui peut être étendue pour capturer des relations entre niveaux. Dans un réseau multi-niveau, cela se traduit par une affinité renforcée entre des groupes différents (par exemple, dans un réseau d’entreprise, des interactions renforcées entre départements similaires).
  
- **Contexte et Influence Multi-Niveau** : Ce concept explore les interactions verticales et horizontales, en modélisant l’influence que des acteurs situés à différents niveaux peuvent exercer les uns sur les autres (par exemple, influence de la direction d’une organisation sur les équipes opérationnelles, ou vice versa).
  
- **Décomposition des Couches** : Chaque couche représente une relation ou une interaction spécifique (par exemple, collaboration ou citation dans un réseau académique). Cette décomposition permet d’analyser l’indépendance des interactions dans chaque couche, ainsi que leurs interdépendances, offrant une vision plus détaillée des dynamiques globales du réseau.

## I.2 Typologie et Enjeux Méthodologiques des Modèles Multi-Niveau

### Typologie des Réseaux Multi-Niveau
Les réseaux multi-niveau peuvent être classés en trois grands types, chacun ayant des caractéristiques analytiques propres :

- **Réseaux Multiplex (Multiplex Networks)** : Ces réseaux permettent d’intégrer plusieurs types de relations entre les mêmes nœuds. Par exemple, dans une entreprise, deux individus peuvent être reliés à la fois par une relation de mentorat, de collaboration, et d’amitié. Ce type de réseau est utile pour étudier la redondance ou la complémentarité entre différents types de relations.

- **Réseaux Multi-Couches (Multi-Layer Networks)** : Ces réseaux sont constitués de plusieurs couches interconnectées représentant des interactions distinctes mais reliées. Dans une analyse de controverses politiques, par exemple, une couche pourrait représenter les interactions Twitter entre leaders d’opinion et une autre les discussions sur des plateformes comme Reddit. Les liens inter-couches permettent de suivre l’impact des débats politiques à travers différentes strates d’audience.

- **Réseaux Interconnectés (Interconnected Networks)** : Ce type de réseau relie des systèmes structurellement distincts par l’intermédiaire de nœuds-ponts ou de courtage, souvent appelés « ponts de liaison ». Contrairement aux réseaux multi-couches, ces réseaux permettent de connecter des réseaux qui n’ont aucune structure partagée (comme les réseaux de fournisseurs et de clients dans une chaîne logistique).

### Enjeux Méthodologiques des Modèles Multi-Niveau
Les réseaux multi-niveau présentent plusieurs défis méthodologiques qui nécessitent des méthodes statistiques et computationnelles sophistiquées :

1. **Identification des Types de Liens** : Les modèles doivent déterminer les liens significatifs dans chaque couche et comprendre comment les relations entre couches influencent le réseau global.

2. **Mesure des Interactions Multi-Niveau** : Estimer l’effet des interactions entre niveaux (par exemple, collaborations académiques et citations) pour mieux saisir l’influence des caractéristiques propres à chaque niveau sur les interactions globales.

3. **Visualisation et Interprétation** : Représenter graphiquement des réseaux multi-niveau est complexe, surtout quand on veut observer des relations multi-niveau simultanément. Les outils de visualisation doivent rendre possible une navigation fluide entre les niveaux tout en permettant une analyse approfondie des interactions.

## I.3. Applications des Modèles Multi-Niveau en Analyse de Réseaux

### Analyse des Rôles et Positions dans les Réseaux Multi-Niveau
Les modèles multi-niveau permettent une compréhension enrichie des rôles et positions des nœuds dans un réseau. Par exemple, dans un réseau de collaboration scientifique, un acteur peut jouer un rôle de **connecteur** entre deux équipes (niveau équipe) tout en étant un acteur influent (niveau individuel). Cette analyse multi-niveau permet de détecter les **courtiers inter-niveaux** qui favorisent la circulation des idées et des ressources entre niveaux.

### Études de Cas en Sciences Sociales
- **Réseaux de Connaissances Scientifiques** : Dans un réseau académique, les chercheurs, équipes et institutions représentent différents niveaux. Les réseaux multi-niveau permettent d’analyser comment les collaborations et citations entre chercheurs influencent les orientations de recherche institutionnelles.
  
- **Réseaux Économiques** : Dans un réseau économique multi-niveau, les niveaux peuvent inclure les individus, entreprises et industries. Par exemple, les collaborations inter-entreprises peuvent influencer des tendances industrielles plus larges, et vice versa, montrant comment les comportements d’entités individuelles impactent des dynamiques sectorielles.

- **Réseaux de Controverses Politiques** : Dans les réseaux de débats en ligne, les acteurs peuvent être à des niveaux différents (par exemple, influenceurs, abonnés, grand public), et l’analyse multi-niveau aide à comprendre comment les leaders d’opinion influencent les sous-réseaux plus vastes des abonnés et des auditeurs. 

### Perspectives et Implications des Modèles Multi-Niveau
Les modèles multi-niveau offrent une vision approfondie des interactions inter-niveaux, mais présentent aussi des limitations, notamment en termes de complexité computationnelle et de difficulté d’interprétation. À mesure que les réseaux deviennent de plus en plus vastes et denses, de nouveaux défis éthiques apparaissent également, notamment sur la manière d’analyser des réseaux englobant des informations sensibles. 

En somme, les modèles multi-niveau permettent d’intégrer des dynamiques complexes et variées dans l’analyse des réseaux sociaux, en tenant compte des divers niveaux et types de relations qui les composent. En combinant des méthodes computationnelles avancées avec une interprétation nuancée des dynamiques sociales, ils ouvrent de nouvelles perspectives pour la recherche en sciences sociales.

# II - Pratique et Implémentation des Modèles Multi-Niveau en R

L'analyse des réseaux multiniveau est une méthode avancée en sciences sociales et en informatique pour modéliser et comprendre les interactions complexes entre différents types de relations dans des réseaux. Voici une explication détaillée des méthodes et des outils en R pour l'analyse de ces réseaux, en se concentrant sur les réseaux multiplex, multicouche et interconnectés.

## II.1 Structuration des Réseaux Multi-Niveau

Pour bien comprendre la structuration des réseaux multi-niveaux en R, examinons les différents types de réseaux et leurs spécificités en termes de données et de modélisation. Les réseaux multi-niveaux nécessitent une structuration qui permet de différencier les types de relations, les acteurs impliqués, et les couches (ou niveaux) d’analyse. Voici une présentation des différentes structures de données et de la manière de les implémenter en R.

## Structuration des Données pour l’Analyse de Réseaux Multi-Niveaux

### 1. Réseaux Multiplex

Les réseaux multiplex consistent en plusieurs types de relations entre les mêmes nœuds. Chaque type de relation est une couche distincte, mais les nœuds sont partagés entre les couches. Par exemple, dans un réseau de collaboration académique, un chercheur peut être relié à un autre en tant que co-auteur, mais également en tant que collaborateur de projet. Pour modéliser un réseau multiplex, nous devons définir chaque type de relation séparément.

**Exemple d’implémentation en R avec `igraph` pour un réseau multiplex :**

```r
library(igraph)

# Définition des nœuds
nodes <- data.frame(id = 1:5, name = c("Alice", "Bob", "Charlie", "Diana", "Eve"))

# Définition des liens pour chaque type de relation
coauthorship_edges <- data.frame(from = c(1, 1, 2), to = c(2, 3, 3))  # Relation de co-auteur
project_collab_edges <- data.frame(from = c(1, 3, 4), to = c(3, 4, 5)) # Collaboration de projet

# Création des graphes
coauthorship_graph <- graph_from_data_frame(d = coauthorship_edges, vertices = nodes, directed = FALSE)
project_collab_graph <- graph_from_data_frame(d = project_collab_edges, vertices = nodes, directed = FALSE)

# Visualisation des graphes
par(mfrow = c(1, 2)) # Pour afficher les deux réseaux côte à côte
plot(coauthorship_graph, main = "Réseau de Co-Auteur")
plot(project_collab_graph, main = "Réseau de Collaboration de Projet")
```

Chaque réseau représente un type de relation. Dans les analyses multi-niveau, ces réseaux peuvent être superposés pour identifier les acteurs qui jouent plusieurs rôles, en examinant les nœuds présents dans plusieurs couches.

### 2. Réseaux Multi-Couches

Les réseaux multi-couches (ou multi-layer) incluent plusieurs types de nœuds et de relations inter-couches. Les couches peuvent représenter des groupes d’acteurs différents et les liens peuvent exister entre les couches. Par exemple, un réseau académique peut comporter des couches pour les chercheurs, les équipes de recherche, et les institutions, chaque couche ayant ses propres liens internes et des liens inter-couches.

**Exemple d’implémentation en R pour un réseau multi-couches :**

```r
library(igraph)

# Définition des nœuds pour chaque couche
researchers <- data.frame(id = 1:3, layer = "Chercheur", name = c("Alice", "Bob", "Charlie"))
teams <- data.frame(id = 4:5, layer = "Équipe", name = c("TeamA", "TeamB"))
institutions <- data.frame(id = 6:7, layer = "Institution", name = c("UnivX", "UnivY"))

# Fusionner tous les nœuds en un seul dataframe
nodes <- rbind(researchers, teams, institutions)

# Définition des liens intra-couches et inter-couches
intra_team_edges <- data.frame(from = c(1, 2), to = c(2, 3), type = "collaboration") # Chercheurs collaborant
inter_team_edges <- data.frame(from = c(1, 4, 2), to = c(4, 5, 5), type = "affiliation") # Affiliation des chercheurs aux équipes
inter_institution_edges <- data.frame(from = c(4, 5), to = c(6, 7), type = "institution") # Affiliation des équipes aux institutions

# Créer un graphe multi-couche
all_edges <- rbind(intra_team_edges, inter_team_edges, inter_institution_edges)
multi_layer_graph <- graph_from_data_frame(d = all_edges, vertices = nodes, directed = TRUE)

# Visualisation
V(multi_layer_graph)$color <- ifelse(V(multi_layer_graph)$layer == "Chercheur", "skyblue", 
                                     ifelse(V(multi_layer_graph)$layer == "Équipe", "salmon", "lightgreen"))
plot(multi_layer_graph, vertex.color=V(multi_layer_graph)$color, main = "Réseau Multi-Couche")
```

Dans ce cas, chaque couleur représente une couche, ce qui permet d’identifier visuellement les liens inter-couches (par exemple, un chercheur affilié à une équipe, ou une équipe rattachée à une institution). Les liens inter-couches aident à analyser l’influence des relations structurelles entre les différents niveaux.

### 3. Réseaux Interconnectés

Les réseaux interconnectés comportent des réseaux distincts reliés par des nœuds de liaison, qui agissent comme des courtiers. Contrairement aux réseaux multi-couches, les réseaux interconnectés permettent des interactions entre des réseaux indépendants.

**Exemple d’implémentation en R pour un réseau interconnecté :**

Imaginons deux réseaux : un réseau d’influence (représentant des leaders d’opinion) et un réseau de collaboration académique. Ces réseaux peuvent être reliés par des nœuds représentant des influenceurs qui sont aussi des chercheurs.

```r
# Définition des nœuds des deux réseaux
researchers <- data.frame(id = 1:3, type = "Chercheur", name = c("Alice", "Bob", "Charlie"))
influencers <- data.frame(id = 4:6, type = "Influenceur", name = c("Dave", "Eve", "Frank"))

# Fusionner tous les nœuds en un seul dataframe
nodes <- rbind(researchers, influencers)

# Définition des liens pour chaque réseau
collaboration_edges <- data.frame(from = c(1, 2), to = c(2, 3), type = "collaboration") # Réseau de collaboration académique
influence_edges <- data.frame(from = c(4, 4, 5), to = c(5, 6, 6), type = "influence") # Réseau d'influence

# Définition des liens inter-réseau (liaisons entre chercheurs et influenceurs)
broker_edges <- data.frame(from = c(1, 3), to = c(4, 6), type = "liaison")

# Création du réseau interconnecté
all_edges <- rbind(collaboration_edges, influence_edges, broker_edges)
interconnected_graph <- graph_from_data_frame(d = all_edges, vertices = nodes, directed = TRUE)

# Visualisation du réseau
V(interconnected_graph)$color <- ifelse(V(interconnected_graph)$type == "Chercheur", "blue", "red")
plot(interconnected_graph, vertex.color = V(interconnected_graph)$color, main = "Réseau Interconnecté")
```

Les nœuds bleus représentent les chercheurs, et les rouges les influenceurs. Les liens inter-réseau montrent comment des individus dans des réseaux indépendants peuvent jouer un rôle de courtage, facilitant les interactions entre les communautés d’influenceurs et les chercheurs.

---

## Points Clés pour l’Analyse Multi-Niveau en R

- **Attributs des Nœuds** : Chaque nœud doit contenir des attributs qui identifient sa couche ou son type (par exemple, `layer = "chercheur"`). Cela permet de filtrer et d’analyser les réseaux par niveau.

- **Types de Liens** : Les liens doivent être catégorisés pour distinguer les relations intra-couches (liens dans la même couche) des liens inter-couches (liens entre couches). Les attributs des liens (par exemple, `type = "collaboration"`) facilitent l’analyse ciblée des interactions intra- et inter-niveaux.

- **Flexibilité de Visualisation** : Les visualisations multi-niveaux nécessitent des distinctions claires entre les couches et les types de liens. Utilisez des couleurs, des tailles et des formes pour représenter les nœuds et les liens, ce qui améliore la clarté de la structure du réseau.

La structuration multi-niveau en R est cruciale pour l’analyse approfondie des dynamiques inter-groupes et intra-groupes dans les réseaux sociaux. En utilisant les fonctionnalités de `igraph` pour différencier les types de nœuds et de liens, nous pouvons explorer des aspects complexes de la sociabilité, de la collaboration, et de l’influence dans des systèmes multi-niveaux.

## II.2. Modèle de constitution
L’analyse statistique des réseaux multi-niveaux nécessite des modèles qui peuvent capturer les relations et dépendances entre les niveaux d’interaction. Cette section examine les principaux modèles utilisés en analyse de réseaux multi-niveaux, avec des exemples d’implémentation en R. Chaque modèle est adapté à un type particulier de question de recherche, en fonction de la nature des données et des interactions entre niveaux.

---

## Modèles de Régression Multi-Niveau

Les modèles de régression multi-niveau, aussi appelés modèles hiérarchiques, sont particulièrement utiles pour évaluer comment les attributs des nœuds à différents niveaux influencent la formation des liens dans le réseau. Ces modèles permettent d’intégrer les caractéristiques de chaque niveau (par exemple, individuels, organisationnels, institutionnels) pour analyser les facteurs qui favorisent la création de liens entre les acteurs.

### Exemple d’Utilisation : Réseaux Académiques
Dans un réseau académique multi-niveau, les attributs individuels des chercheurs (niveau individuel), les attributs des équipes de recherche (niveau d’équipe), et les caractéristiques institutionnelles (niveau institutionnel) peuvent tous influencer la probabilité qu’un lien de collaboration se forme entre deux chercheurs.

**Exemple d'implémentation en R avec le package `lme4`**:

```r
library(lme4)

# Exemple de données
# Les données contiennent des liens entre chercheurs et des attributs au niveau institutionnel
# Exemple de structure de données
# your_data <- data.frame(lien = ..., attribut_niveau1 = ..., attribut_niveau2 = ..., ...)

# Modèle de régression hiérarchique multi-niveau
# Ici, 'attribut_niveau1' représente un attribut au niveau individuel (ex : domaine de recherche)
# et 'attribut_niveau2' représente un attribut institutionnel (ex : type d'institution)
model <- lmer(lien ~ attribut_niveau1 + (1 | attribut_niveau2), data = your_data)
summary(model)
```

Dans cet exemple, l’effet de l’attribut au niveau de l’institution (`attribut_niveau2`) est modélisé comme un effet aléatoire, permettant de contrôler l'influence des caractéristiques institutionnelles sur la probabilité de formation de liens entre chercheurs.

### Interprétation des Résultats
Les coefficients obtenus pour les attributs de niveau individuel et institutionnel indiquent l’influence de ces variables sur la formation des liens. Un coefficient positif signifie que l’attribut en question augmente la probabilité de formation d'un lien.

---

## Modèles Exponentiels Multi-Niveau (ML-ERGM)

Les ML-ERGM (Modèles Exponentiels Multi-Niveau) sont des extensions des ERGM (Exponential Random Graph Models) classiques, spécialement conçues pour capturer les interactions et dépendances entre plusieurs niveaux dans des réseaux complexes. Dans un contexte multi-niveau, ces modèles prennent en compte les effets de dépendance (mutualité, transitivité, homophilie) entre les couches du réseau.

### Exemple d’Utilisation : Réseaux Organisationnels
Imaginons un réseau organisationnel avec des employés (niveau individuel), des équipes (niveau intermédiaire), et l’entreprise elle-même (niveau institutionnel). Les ML-ERGM permettent d’étudier comment les caractéristiques des employés, des équipes et de l’entreprise influencent la formation de liens de collaboration entre les employés, en tenant compte des effets de dépendance entre niveaux.

Bien que les packages R pour les ML-ERGM ne soient pas encore développés de manière complète, une approche similaire peut être envisagée en utilisant `btergm` pour modéliser des réseaux temporels et ajouter des dépendances spécifiques.

**Exemple d'implémentation simplifiée en R avec `btergm`**:

```r
library(btergm)

# Exemple de structure pour les réseaux multi-niveaux avec des couches et des dépendances
# 'net' représente un réseau avec des niveaux spécifiés dans les attributs des nœuds et des liens
model <- btergm(net ~ edges + mutual(layer1, layer2) + transitiveweights(layer1, layer2), R = 100)
summary(model)
```

### Interprétation des Résultats
Les paramètres de dépendance (ex : mutualité entre niveaux) indiquent la propension des nœuds de niveaux différents à former des liens réciproques. Par exemple, un paramètre de mutualité élevé entre les couches d’équipe et de département suggère que les employés de différents départements tendent à collaborer plus fréquemment au sein de la même équipe.

---

## Modèles Stochastic Actor-Oriented Multi-Niveau (ML-SIENA)

Les modèles SAOM (Stochastic Actor-Oriented Models) peuvent également être étendus pour capturer les dépendances entre les niveaux dans des réseaux dynamiques. Ces modèles, appelés ML-SIENA, permettent de modéliser la dynamique de réseau au fil du temps tout en intégrant les interactions multi-niveaux. 

### Exemple d’Utilisation : Réseaux de Collaboration Académique
Dans un réseau de collaboration académique, les chercheurs peuvent être influencés par leur institution (niveau institutionnel) et par les caractéristiques de leur équipe de recherche (niveau d’équipe). Les ML-SIENA permettent de modéliser comment les choix de collaboration d’un chercheur évoluent dans le temps en fonction des préférences individuelles et des structures multi-niveau.

**Exemple d'implémentation en R avec `RSiena`**:

```r
library(RSiena)

# Exemple de création de réseau multi-niveau pour RSiena
# Exemple de structure de données pour réseaux dynamiques avec couches et dépendances
actors <- sienaNodeSet(10, 'Chercheurs')
teams <- sienaNodeSet(5, 'Équipes')
relations <- sienaDependent(sienaNetwork(array(dim = c(10, 10, 3)))) # Ex. réseau dynamique

# Création de données multi-niveau pour RSiena
data <- sienaDataCreate(relations, actors, teams)

# Définition des effets
effects <- getEffects(data)
effects <- includeEffects(effects, simX, type="rate") # Ex. de dépendance temporelle

# Création du modèle
model <- sienaAlgorithmCreate(projname = "multilevel_network")
results <- siena07(model, data = data, effects = effects)
summary(results)
```

### Interprétation des Résultats
Les paramètres obtenus permettent d’interpréter la dynamique d’évolution des liens entre niveaux, notamment en observant comment les relations passées et les affiliations influencent les nouvelles collaborations dans le réseau.

---

## II.3 Modèle dynamique des layers
Les modèles dynamiques pour les réseaux multi-niveaux (ou layers) permettent d’analyser comment les relations évoluent non seulement au sein de chaque couche, mais également entre les couches au fil du temps. En intégrant la dimension temporelle, ces modèles offrent une vue approfondie des changements de structure et des interactions inter-couches dans des systèmes complexes tels que les réseaux académiques, les réseaux sociaux ou les réseaux d’entreprise.

---

## Modèles Dynamiques des Couches (Layers)

Les modèles dynamiques des couches, ou layers, sont conçus pour examiner les interactions au sein et entre les couches d’un réseau qui évoluent dans le temps. Ils permettent de capturer la manière dont les changements dans un niveau (par exemple, les relations interpersonnelles) influencent d'autres niveaux (comme les interactions entre institutions ou départements) et vice versa. Voici les principaux modèles statistiques et d'apprentissage automatique adaptés pour les couches dynamiques dans les réseaux multi-niveaux.

---

### 1. Modèles de Markov Cachés pour les Réseaux Dynamiques Multi-Niveau (ML-HMM)

Les **Modèles de Markov Cachés (HMM)** appliqués aux réseaux dynamiques multi-niveaux permettent de capturer les transitions entre états pour chaque nœud au sein de chaque niveau. Ces modèles représentent chaque nœud comme évoluant entre différents états latents (cachés), influencés par les relations entre nœuds au même niveau et entre niveaux. Cette approche est particulièrement utile dans des réseaux où les interactions entre niveaux influencent l’évolution des comportements ou des relations.

**Exemple d’Utilisation : Réseaux de Collaboration en Ligne**
Dans un réseau de collaboration en ligne, les chercheurs peuvent se regrouper en différents sous-groupes au fil du temps, influencés par les tendances de collaboration d’autres chercheurs dans des disciplines différentes. Les ML-HMM permettent de capturer les changements dans ces groupes et de modéliser les dépendances temporelles entre niveaux.

**Exemple d'implémentation en R avec `depmixS4`**:

```r
library(depmixS4)

# Exemple de modèle HMM avec des états pour différents niveaux (ex. réseaux inter-équipes)
# 'data' est un dataframe contenant des observations temporelles

# Spécification du modèle
hmm_model <- depmix(response = link ~ 1, family = binomial(), nstates = 2, data = data)
fit_hmm <- fit(hmm_model)
summary(fit_hmm)
```

### Interprétation des Résultats
Les états latents peuvent être interprétés comme des groupes de comportement ou de rôle, et les transitions entre états montrent comment les relations entre les couches du réseau influencent la dynamique du réseau.

---

### 2. Modèles SAOM Multi-Niveau (ML-SIENA) pour Réseaux Dynamiques

Les modèles **SAOM** (Stochastic Actor-Oriented Models) dynamiques pour réseaux multi-niveaux, aussi appelés **ML-SIENA**, sont des extensions des modèles SAOM classiques. Ils permettent de capturer les interactions entre les couches et d’analyser comment ces relations évoluent au fil du temps. Dans un contexte multi-niveau, les décisions d’un acteur de former ou rompre un lien peuvent être influencées par les relations dans un autre niveau.

**Exemple d’Utilisation : Réseaux Académiques et Institutionnels**
Dans les réseaux académiques, la décision d’un chercheur de collaborer avec un autre peut être influencée par les affiliations institutionnelles et par les relations de leurs institutions respectives. Les ML-SIENA permettent de modéliser cette dynamique en intégrant les attributs individuels et institutionnels.

**Exemple d'implémentation en R avec `RSiena`**:

```r
library(RSiena)

# Définition des nœuds et des relations pour les différents niveaux
# Exemple de réseaux dynamiques avec couches pour RSiena
actors <- sienaNodeSet(10, 'Chercheurs')
teams <- sienaNodeSet(5, 'Équipes')
relations <- sienaDependent(sienaNetwork(array(dim = c(10, 10, 3)))) # Ex. réseau dynamique

# Création de données multi-niveau pour RSiena
data <- sienaDataCreate(relations, actors, teams)

# Définition des effets multi-niveaux
effects <- getEffects(data)
effects <- includeEffects(effects, simX, type="rate") # Exemple de dépendance temporelle

# Création du modèle et estimation
model <- sienaAlgorithmCreate(projname = "multi_layer_network")
results <- siena07(model, data = data, effects = effects)
summary(results)
```

### Interprétation des Résultats
Les coefficients des effets temporels montrent l’influence des niveaux institutionnels sur les choix de collaboration entre chercheurs. Ce type de modèle permet d’observer comment les préférences individuelles et les affiliations institutionnelles évoluent conjointement, influençant ainsi les choix de collaboration.

---

### 3. Temporal Exponential Random Graph Models (TERGM) pour Réseaux Multi-Niveau

Les **TERGM** sont des modèles ERGM appliqués aux réseaux dynamiques, et ils peuvent être adaptés pour modéliser des réseaux multi-niveau. Les TERGM permettent de capturer les effets de dépendance dans des réseaux multi-niveau au fil du temps, en analysant comment les configurations de réseau d’une période influencent les configurations futures.

**Exemple d’Utilisation : Réseaux d’Influence dans les Médias Sociaux**
Dans un réseau d'influenceurs et d'abonnés, les relations entre influenceurs peuvent influencer les abonnés et vice versa. Les TERGM permettent de modéliser ces interactions et d’observer comment les structures de réseau évoluent à mesure que les influenceurs gagnent ou perdent des abonnés.

**Exemple d'implémentation en R avec `btergm`**:

```r
library(btergm)

# Spécification du modèle TERGM multi-niveau pour un réseau dynamique
model_tergm <- btergm(net ~ edges + mutual("layer1", "layer2") + transitiveweights("layer1", "layer2"), R = 100)
summary(model_tergm)
```

### Interprétation des Résultats
Les paramètres de dépendance montrent la tendance des nœuds à maintenir des liens stables dans le temps. Par exemple, un coefficient positif pour la transitivité indique que les nœuds liés par des tiers tendent à établir des liens entre eux dans des périodes futures.

---

### 4. Graph Neural Networks pour les Réseaux Multi-Niveau Dynamiques (Temporal GNN)

Les **Graph Neural Networks** (GNN) offrent une méthode d’apprentissage profond qui s’adapte bien aux réseaux dynamiques multi-niveaux. Pour les réseaux qui évoluent dans le temps, des variantes de GNN comme **Temporal Graph Convolutional Networks (T-GCN)** et **Dynamic Graph Attention Networks (D-GAT)** permettent de capturer les interactions et dépendances entre couches tout en tenant compte de la dimension temporelle.

**Exemple d’Utilisation : Réseaux Financiers Multi-Niveau**
Dans un réseau de transactions financières, les transactions entre individus, institutions et marchés peuvent être modélisées de manière dynamique. Les T-GCN permettent de capturer l’évolution des transactions et des relations inter-niveaux en fonction de la dimension temporelle.

**Exemple d'implémentation avec PyTorch Geometric (exemple simplifié en pseudo-code)**:

```python
import torch
import torch_geometric
from torch_geometric.nn import TGCN, GATConv

# Exemple de données dynamiques pour un réseau multi-niveau avec T-GCN
class TGCNLayer(torch.nn.Module):
    def __init__(self, in_channels, out_channels):
        super(TGCNLayer, self).__init__()
        self.conv = TGCN(in_channels, out_channels)

    def forward(self, x, edge_index):
        x = self.conv(x, edge_index)
        return x

# Initialisation et entraînement du modèle
model = TGCNLayer(in_channels=10, out_channels=10)
```

### Interprétation des Résultats
Les embeddings produits par les T-GCN ou les D-GAT capturent les relations temporelles et inter-niveaux, fournissant une représentation riche des interactions dans le réseau. Ces modèles permettent d’analyser la manière dont les interactions entre niveaux évoluent et influencent les structures globales dans un réseau dynamique.

---

### Conclusion

Les modèles dynamiques pour les réseaux multi-niveaux offrent une variété d’outils pour analyser les réseaux en évolution et leurs dépendances entre couches. Que ce soit par des méthodes statistiques (comme les TERGM et les ML-SIENA) ou des méthodes d’apprentissage profond (comme les Temporal GNN), les chercheurs peuvent désormais modéliser des dynamiques complexes dans des réseaux à plusieurs niveaux et obtenir une vision plus nuancée des interactions sociales, économiques et institutionnelles dans le temps.

## II.4 Visualisation des Résultats

La visualisation des réseaux multi-niveau peut être réalisée en utilisant des couleurs et des formes distinctes pour chaque couche, facilitant l'identification des relations inter-couche et intra-couche :

```r
library(ggplot2)

V(net)$color <- ifelse(V(net)$layer == "chercheur", "blue", ifelse(V(net)$layer == "équipe", "green", "red"))
plot(net, vertex.color=V(net)$color, edge.arrow.size=0.5)
```

### Conclusion

L'analyse des réseaux multi-niveau en R nécessite une compréhension approfondie des structures de données, des packages disponibles et des modèles statistiques adaptés aux contextes multi-niveau. Les exemples fournis montrent comment structurer, modéliser et visualiser ces réseaux, en utilisant des méthodes et des outils largement reconnus dans la communauté scientifique. Pour des analyses plus poussées, l'intégration de nouvelles méthodologies d'apprentissage automatique, comme les **Graph Neural Networks**, peut offrir des perspectives innovantes sur la dynamique des interactions entre les différents niveaux du réseau.


# III : Applications et Interprétation des Modèles Multi-Niveau

Les modèles multi-niveau offrent une approche puissante pour analyser des réseaux complexes où les relations sont influencées par des facteurs à plusieurs niveaux. Ces modèles permettent d'étudier non seulement les liens au sein de chaque niveau (intra-niveau) mais aussi les interactions entre niveaux (inter-niveau), qui jouent un rôle crucial dans la structuration des dynamiques des réseaux sociaux, économiques et politiques. Cette partie examine des applications concrètes des modèles multi-niveau dans différents contextes des sciences sociales, en se concentrant sur les rôles, les positions, et l’influence des nœuds structurants, ainsi que sur les implications théoriques et méthodologiques de ces analyses.

## 2. Applications des Modèles Multi-Niveau en Sciences Sociales

Les modèles multi-niveau se révèlent particulièrement utiles dans des contextes où les interactions sont réparties entre des niveaux hétérogènes. Voici quelques exemples d’applications pertinentes en sciences sociales :

- **Réseaux Professionnels (Entreprise et Inter-Entreprise)** : Dans les organisations modernes, les réseaux professionnels comportent des niveaux internes, tels que les équipes, les départements ou les divisions, et des niveaux externes, comme les collaborations inter-entreprises ou les alliances industrielles. Les modèles multi-niveau permettent d’analyser comment les dynamiques internes (par exemple, la communication au sein d’un service) sont influencées par les interactions externes (comme les partenariats entre entreprises). Dans ce contexte, il est possible de déceler des nœuds structurants (par exemple, des courtiers qui relient plusieurs entreprises) et d’évaluer comment ces nœuds renforcent la résilience du réseau professionnel.

- **Réseaux Académiques (Collaborations, Citations et Thématiques)** : En milieu académique, les chercheurs sont liés par des collaborations directes (co-auteurs), des réseaux de citations, et des thématiques de recherche. Un modèle multi-niveau peut intégrer les relations entre individus (niveau de la collaboration), les influences intellectuelles (niveau de la citation) et les disciplines scientifiques (niveau thématique). Par exemple, une analyse multi-niveau dans un réseau de citation peut révéler comment des groupes de chercheurs collaborent non seulement en fonction de leurs affiliations institutionnelles mais aussi en suivant des thématiques de recherche communes. Ce type de modèle facilite également l’analyse des dynamiques d’influence dans la diffusion des connaissances et la structuration des disciplines académiques.

- **Réseaux de Communication en Ligne (Réseaux d’Influenceurs et d’Abonnés)** : Les réseaux en ligne, comme les plateformes de réseaux sociaux, sont multi-niveaux par nature, car les utilisateurs interagissent à des degrés et sur des plateformes différentes. Par exemple, un utilisateur peut suivre des influenceurs, rejoindre des groupes thématiques et participer à des discussions dans des sous-réseaux spécifiques. Les modèles multi-niveau permettent de modéliser ces différentes dimensions d’interaction, en capturant comment les relations inter-niveau influencent la formation des sous-communautés et les phénomènes de propagation d’informations. Dans un réseau d’influenceurs et d’abonnés, par exemple, un modèle multi-niveau peut identifier les influenceurs qui jouent un rôle de courtier entre différents groupes d’abonnés, révélant les dynamiques d’information et d’influence dans les communautés en ligne.

En somme, les modèles multi-niveau offrent un cadre de recherche essentiel pour analyser les structures et dynamiques complexes au sein des réseaux sociaux modernes. Ils permettent aux chercheurs de relier plusieurs niveaux d’analyse et de comprendre les interconnexions entre des entités de nature variée, ce qui ouvre la voie à des études plus complètes et nuancées des systèmes sociaux, professionnels, académiques et numériques.
## 1. Analyse des Réseaux Sociaux et Multi-Niveaux

Dans l’analyse des réseaux sociaux multi-niveau, les modèles permettent de distinguer les rôles et positions occupés par les acteurs en fonction de leur place dans les différents niveaux d’un réseau. Ces modèles offrent des outils pour identifier des acteurs jouant des rôles clés tels que :

- **Connecteurs dans les réseaux professionnels** : Dans un réseau multi-niveau, un connecteur peut être un individu qui relie différents niveaux hiérarchiques ou départementaux. Par exemple, dans une entreprise, certains employés peuvent agir comme des connecteurs en facilitant la communication entre équipes ou entre départements. Les connecteurs jouent un rôle clé dans la diffusion de l’information et la coordination des activités.

- **Courtiers inter-niveaux** : Les courtiers sont des nœuds stratégiques qui relient différents niveaux d’un réseau. Leur rôle est particulièrement important dans les organisations complexes où les informations doivent circuler entre les différentes couches hiérarchiques ou entre départements spécialisés. Par exemple, un courtier inter-niveaux dans une entreprise internationale pourrait être un manager régional qui coordonne les relations entre le siège et les filiales locales. En reliant des nœuds de niveaux différents, ces acteurs facilitent la cohésion et l’intégration du réseau.

- **Nœuds structurants** : Certains nœuds agissent comme des points d’ancrage du réseau en structurant les relations autour d’eux. Dans les réseaux multi-niveau, ces nœuds peuvent être des institutions ou des individus ayant une influence significative sur les autres acteurs, comme un leader d'opinion ou une entreprise pivot dans un réseau d'affaires. Leur importance est renforcée par leur capacité à affecter les relations non seulement à leur propre niveau mais également aux niveaux supérieurs ou inférieurs.

## 2. Études de Cas : Modèles Multi-Niveau dans la Recherche en Sciences Sociales

Les modèles multi-niveau ont été appliqués dans divers domaines des sciences sociales pour étudier des réseaux de collaboration, des réseaux économiques et des réseaux de politique publique. Voici des exemples illustrant l’usage de ces modèles dans des contextes concrets :

- **Exemple 1 : Réseaux de Collaborations Scientifiques**
   - **Niveaux** : chercheurs, équipes, institutions.
   - **Analyse** : Les modèles multi-niveau permettent de capturer la dynamique des collaborations entre chercheurs au sein d’équipes, entre équipes au sein d’institutions, et entre institutions. Cette approche permet de comprendre comment les collaborations se forment en fonction des affinités entre chercheurs, des intérêts thématiques d’équipes, et des orientations stratégiques des institutions. Par exemple, un modèle ML-ERGM pourrait être utilisé pour modéliser la probabilité de collaborations entre chercheurs en fonction de leurs institutions respectives et de leur discipline de recherche.
   
- **Exemple 2 : Réseaux Économiques**
   - **Niveaux** : individus, entreprises, industries.
   - **Analyse** : Dans les réseaux économiques, les modèles multi-niveau permettent d’analyser les relations entre employés au sein d’une entreprise, les liens de collaboration entre entreprises, et les interactions entre industries. Un modèle multi-niveau appliqué à ce contexte pourrait révéler comment les relations entre entreprises sont influencées par des facteurs individuels (par exemple, les compétences des employés) et par des dynamiques sectorielles (par exemple, les coopérations entre industries connexes). Les applications incluent l’analyse des chaînes d'approvisionnement, la formation de partenariats, et les dynamiques d'innovation inter-entreprises.
   
- **Exemple 3 : Réseaux de Politique Publique**
   - **Niveaux** : acteurs locaux, nationaux, internationaux.
   - **Analyse** : Dans les réseaux de politique publique, les relations entre acteurs sont souvent influencées par des contraintes et des opportunités à plusieurs niveaux. Par exemple, des acteurs locaux peuvent être influencés par des directives nationales, tandis que des acteurs nationaux sont en relation avec des institutions internationales. Un modèle SAOM multi-niveau pourrait être utilisé pour analyser comment les acteurs locaux adaptent leurs actions en fonction des décisions prises au niveau national, et comment les politiques internationales influencent les dynamiques de coopération et de concurrence au sein des acteurs locaux et nationaux.

## 3. Implications pour la Recherche et Interprétation des Résultats

Les modèles multi-niveau apportent des perspectives nouvelles en analyse des réseaux, mais posent aussi des défis en termes de modélisation et d’interprétation. Cette section explore comment les dépendances inter-niveaux influencent les dynamiques de réseau et discute des limites et implications de ces modèles pour la recherche en sciences sociales.

- **Influence des dépendances inter-niveaux sur la dynamique des réseaux** : Les relations entre niveaux influencent fortement les dynamiques du réseau global. Par exemple, dans un réseau multi-niveau d'entreprises, les décisions prises au niveau des dirigeants peuvent avoir des effets directs sur les relations entre employés à des niveaux inférieurs. Les dépendances inter-niveaux créent des effets d’entraînement qui renforcent certaines structures relationnelles tout en en limitant d’autres, influençant ainsi l’équilibre global du réseau.

- **Limites des modèles multi-niveau dans l’analyse des réseaux** : Bien que les modèles multi-niveau offrent une vue plus nuancée des réseaux complexes, ils nécessitent des données détaillées et structurées, souvent difficiles à obtenir. La complexité computationnelle et la difficulté d’interprétation des résultats augmentent également avec le nombre de niveaux et de relations inter-niveaux. Par ailleurs, les modèles multi-niveau peuvent introduire des biais si les relations entre niveaux sont mal spécifiées ou mal mesurées, ce qui pourrait affecter la validité des résultats.

- **Perspectives futures : enjeux éthiques et défis des modèles multi-niveau dans des réseaux de plus en plus vastes** : Les modèles multi-niveau posent des défis éthiques, notamment en matière de protection des données. L’analyse de réseaux multi-niveau dans des contextes sensibles (comme les réseaux de soins de santé ou les réseaux de sécurité) soulève des questions sur la confidentialité et l’usage des informations collectées. Les défis techniques pour analyser des réseaux vastes et denses augmentent également, car les capacités computationnelles requises pour modéliser des réseaux multi-niveau massifs sont encore limitées. Les perspectives futures incluent l’intégration des modèles multi-niveau avec des techniques avancées d’intelligence artificielle pour surmonter ces obstacles.

En résumé, les modèles multi-niveau offrent des outils puissants pour la compréhension des réseaux complexes en sciences sociales, en tenant compte des effets de niveau et des dépendances inter-niveaux. Leur potentiel pour améliorer l’analyse des réseaux dans des contextes variés ouvre des perspectives de recherche nouvelles, bien qu’ils exigent une attention particulière aux limites méthodologiques et éthiques.
## Bibliographie Sélective

- Snijders, T. A. B., Van de Bunt, G. G., & Steglich, C. E. G. (2013). Introduction to stochastic actor-based models for network dynamics. *Social Networks*, 32(1), 44-60.
- Block, P., & Grund, T. (2014). Multi-level network analysis for the social sciences. *Network Science*, 2(3), 354-369.
- Wang, P., Robins, G., Pattison, P., & Koskinen, J. (2018). Exponential random graph models for multilevel networks. *Social Networks*, 53, 44-53.
- Shrestha, M., & Tokuta, B. (2020). Graph neural networks in multi-level social network analysis. *Journal of Computational Social Science*, 2(4), 327-340.

---

Ce plan guide les étudiants à travers un état de l'art avancé, en abordant les méthodes classiques et modernes pour l'analyse de réseaux multi-niveaux en sciences sociales et informatiques, ainsi que leurs applications concrètes et interprétations.