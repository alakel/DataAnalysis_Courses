Dans l'analyse des réseaux sociaux, l'identification des **communautés** est essentielle pour comprendre les sous-structures et les dynamiques internes des réseaux complexes. Les communautés représentent des groupes de nœuds plus densément connectés entre eux qu'avec le reste du réseau. La détection précise de ces communautés permet de :

- Comprendre les **dynamiques sociales**.
- Analyser la **diffusion de l'information**.
- Identifier les **groupes d'influence**.
- Étudier les **controverses en ligne** et les **factions**.

Ce cours approfondira les méthodes de détection des communautés en :

- Présentant les **algorithmes les plus performants** et reconnus.
- Optimisant le code en R pour une **meilleure performance**.
- Gérant les **paramètres clés** pour obtenir les **meilleurs résultats possibles**.
**Objectifs du Cours**

- **Comprendre** le concept de communauté dans les réseaux sociaux.
- **Connaître** et **appliquer** les algorithmes de détection de communautés les plus performants.
- **Optimiser** le code en R pour une détection efficace des communautés.
- **Gérer** les paramètres des algorithmes pour améliorer les résultats.
- **Interpréter** les résultats et **analyser** les communautés identifiées.

**Le Concept de Communauté dans les Réseaux Sociaux**

Une **communauté** est un sous-ensemble de nœuds dans un réseau où les nœuds sont plus connectés entre eux qu'avec le reste du réseau.

- **Exemples** :
  - Groupes d'amis dans un réseau social.
  - Collaborateurs dans un réseau professionnel.
  - Groupes d'utilisateurs partageant les mêmes intérêts.

**Importance de l'Identification des Communautés**

- **Analyse Sociale** : Comprendre les relations et interactions au sein des groupes.
- **Diffusion de l'Information** : Étudier comment les informations se propagent.
- **Marketing Ciblé** : Identifier des segments pour des campagnes marketing.
- **Étude des Controverses** : Analyser les positions et interactions des groupes opposés.
## 1. Concepts Préliminaires et Manipulations du Réseau

Avant de détecter les communautés, il est essentiel de comprendre les structures et les connexions dans le réseau.

### 1.1. Chemins et Connexions

**Chemin le Plus Court**

Le **chemin le plus court** entre deux nœuds est la séquence de liens la plus courte les reliant.

```R
# Trouver le chemin le plus court entre deux nœuds
shortest_paths(net, from = V(net)[name == "homme"], to = V(net)[name == "événement"], output = "both")
```

**Liens Incidents et Voisins**

- **Liens Incidents** : Les liens connectés à un nœud.

  ```R
  incident(net, V(net)[name == "écriture"], mode = "all")
  ```

- **Voisins** : Les nœuds directement connectés à un nœud.

  ```R
  neighbors(net, V(net)[name == "écriture"], mode = "out")
  ```

**Égo-Réseaux**

Un **égo-réseau** est un sous-graphe centré sur un nœud particulier et ses voisins jusqu'à un certain ordre.

```R
# Égo-réseau d'ordre 3
ego_net <- make_ego_graph(net, order = 3, nodes = V(net)[name == "écriture"], mode = "out")[[1]]
```

### 1.2. Filtrage et Sous-Graphes

**Sous-Graphes par Filtre**

Créer des sous-graphes en filtrant les nœuds selon des attributs spécifiques.

```R
# Filtrer les nœuds appartenant à un groupe spécifique
group_attr <- "Politique"
modality <- "gauche"
node_indices <- which(V(net)[[group_attr]] == modality & !is.na(V(net)[[group_attr]]))
subgraph <- induced_subgraph(net, vids = node_indices)
```

**Composantes Connexes**

Les **composantes connexes** d'un réseau sont des sous-graphes maximaux dans lesquels chaque nœud est accessible depuis n'importe quel autre nœud via des chemins. Autrement dit, il existe un chemin entre chaque paire de nœuds au sein de la même composante. Identifier ces composantes permet de comprendre la structure globale du réseau et de détecter d'éventuelles partitions ou îlots isolés.

```R
# Calculer les composantes connexes du réseau
composantes <- components(net)

# Créer un tableau récapitulatif des composantes 
composantes_table <- data.frame( Composante = seq_len(composantes$no), Taille = composantes$csize ) 

# Initialiser des vecteurs pour stocker les métriques supplémentaires
diametres <- numeric(composantes$no)
degre_moyen <- numeric(composantes$no)

# Parcourir chaque composante pour calculer les métriques
for (i in seq_len(composantes$no)) {
  # Extraire les nœuds de la composante i
  nodes_in_component <- which(composantes$membership == i)
  
  # Créer un sous-graphe de la composante
  subgraph <- induced_subgraph(net, vids = nodes_in_component)
  
  # Calculer le diamètre de la composante
  diametres[i] <- diameter(subgraph, directed = FALSE, unconnected = FALSE)
  
  # Calculer le degré moyen des nœuds
  degre_moyen[i] <- mean(degree(subgraph))
}

# Ajouter les nouvelles métriques au tableau
composantes_table$Diametre <- diametres
composantes_table$Degre_Moyen <- round(degre_moyen, 2)

# Afficher le tableau des composantes 

print(composantes_table)
```

La fonction `components()` calcule les composantes connexes du graphe `net`. Elle renvoie un objet contenant plusieurs informations utiles.

```R
# Afficher l'appartenance de chaque nœud à une composante
composantes$membership
```

`membership` est un vecteur indiquant pour chaque nœud à quelle composante il appartient. Les nœuds appartenant à la même composante partagent le même identifiant numérique.

**Décomposition en Sous-Graphes**

Décomposer le réseau en sous-graphes basés sur les composantes connexes permet d'analyser chaque partie du réseau séparément. Ceci est particulièrement utile pour les réseaux comportant plusieurs composantes disjointes.

```R
# Décomposer le réseau en composantes connexes
comps <- decompose(net, mode = "weak", min.vertices = 3)
```

- **Explication :** La fonction `decompose()` crée une liste de sous-graphes, chacun correspondant à une composante connexe du réseau.
  - `mode = "weak"` : Pour les graphes orientés, cela considère les arêtes sans tenir compte de leur direction (composantes faibles). Pour les graphes non orientés, ce paramètre n'a pas d'effet.
  - `min.vertices = 3` : Spécifie que seules les composantes contenant au moins 3 nœuds sont conservées. Cela permet d'exclure les petites composantes qui peuvent être moins pertinentes pour l'analyse, comme les nœuds isolés ou les paires de nœuds connectés.

Une fois le réseau décomposé, vous pouvez analyser chaque sous-graphe individuellement, ce qui facilite l'exploration des structures internes et la détection de communautés au sein de chaque composante.

En identifiant les composantes connexes et en décomposant le réseau, vous obtenez une vision claire de sa structure globale. Cela constitue une étape préalable importante avant d'appliquer des algorithmes de détection de communautés, car ces algorithmes opèrent généralement au sein de composantes connexes.
## 2. Méthodes de Détection des Communautés

Plusieurs algorithmes existent pour détecter les communautés dans un réseau. Nous allons optimiser le code pour ces algorithmes en gérant les paramètres clés.

### 2.1. Méthodes Basées sur les Cliques

Une **clique** est un sous-graphe complet où chaque nœud est connecté à tous les autres nœuds du sous-graphe.

**Détection des Cliques**

```R
# Trouver toutes les cliques de taille au moins 3
cliques_list <- cliques(net, min = 3)

# Trouver les plus grandes cliques
largest_cliques_list <- largest_cliques(net)

# Taille de la plus grande clique
max_clique_size <- clique_num(net)

# Nombre de cliques maximales (non extensibles)
num_max_cliques <- count_max_cliques(net)

# Distribution des tailles de cliques
clique_size_distribution <- clique_size_hist(net)
```

**Interprétation** :

- Les cliques représentent des groupes fortement connectés.
- Utile pour identifier des groupes cohésifs.
Voici un ajout pour inclure les concepts de **n-cliques** et **k-plex** dans le cours. Ces extensions assouplissent la définition de clique en autorisant une connectivité partielle, ce qui est souvent plus adapté aux réseaux sociaux réels.

Mais dans les réseaux sociaux réels, il est rare de trouver des sous-ensembles de nœuds entièrement interconnectés, comme les cliques strictes. Les **n-cliques** et **k-plex** sont des variations qui permettent une connectivité moins rigide tout en conservant un haut degré de cohésion au sein du sous-groupe. 

- **n-Cliques** : Un n-clique est une extension de la clique classique dans laquelle chaque nœud est connecté aux autres membres de la clique par des chemins d'une longueur maximale de `n`. Par exemple, dans un 2-clique, chaque nœud est à une distance de deux ou moins de tous les autres nœuds de la clique.

- **k-Plex** : Un k-plex est un sous-groupe où chaque nœud est connecté à tous les autres sauf à `k` membres. Cela permet de conserver une structure de groupe cohérente tout en autorisant des "lacunes" de connectivité, ce qui est fréquent dans les réseaux où les liens entre membres peuvent fluctuer.

**Code R pour Identifier les n-Cliques et k-Plex**

```R

# Fonction optimisée pour détecter toutes les n-cliques
detect_ncliques <- function(g, n) {
  n_cliques <- list()  # Liste pour stocker les n-cliques
  
  # Obtenir tous les sous-graphes dans un rayon de n pour chaque nœud
  for (v in V(g)) {
    # Sous-graphe d'ordre n autour du nœud v
    subgraph <- induced_subgraph(g, ego(g, order = n, nodes = v)[[1]])
    
    # Récupérer tous les sous-ensembles de nœuds dans ce sous-graphe
    nodes_in_subgraph <- V(subgraph)$name
    size <- length(nodes_in_subgraph)
    
    if (size >= 2) {
      # Générer les combinaisons possibles de nœuds dans le sous-graphe
      combinations <- combn(nodes_in_subgraph, size, simplify = FALSE)
      
      # Vérification des distances pour chaque sous-ensemble
      for (nodes in combinations) {
        candidate_subgraph <- induced_subgraph(g, nodes)
        pairwise_distances <- distances(candidate_subgraph)
        
        # Vérifier si toutes les paires de nœuds sont atteignables en au plus n étapes
        if (all(pairwise_distances <= n)) {
          # Ajouter le sous-ensemble comme une n-clique s'il n'est pas redondant
          clique_found <- sapply(n_cliques, function(clique) all(nodes %in% clique))
          if (!any(clique_found)) {
            n_cliques <- append(n_cliques, list(nodes))
          }
        }
      }
    }
  }
  
  return(n_cliques)
}

# Exemple d'utilisation pour détecter toutes les 2-cliques
all_n_cliques_2 <- detect_ncliques(net, n = 2)

# Afficher les n-cliques
print(all_n_cliques_2)


# Fonction pour détecter tous les k-plex dans un graphe
find_all_k_plexes <- function(g, k) {
  nodes <- V(g)$name
  k_plexes <- list()
  
  # Boucle pour vérifier chaque combinaison de sous-ensembles de nœuds
  for (size in seq(k + 2, length(nodes))) {  # La taille minimale d'un k-plex est k + 2
    subgraph_combinations <- combn(nodes, size, simplify = FALSE)
    
    for (sub_nodes in subgraph_combinations) {
      # Sous-graphe induit par les nœuds du sous-ensemble
      subgraph <- induced_subgraph(g, sub_nodes)
      degrees_in_subgraph <- degree(subgraph)
      
      # Vérification de la condition du k-plex
      if (all(degrees_in_subgraph >= (size - k - 1))) {
        k_plexes <- append(k_plexes, list(sub_nodes))
      }
    }
  }
  
  return(k_plexes)
}

# Exemple d'utilisation avec un 1-plex
all_1_plexes <- find_all_k_plexes(net, k = 1)

# Afficher les k-plexes détectés
print(all_1_plexes)

```

**Interprétation des Résultats**

- **n-Cliques** : Une fois identifiées, les n-cliques peuvent être analysées pour évaluer la cohésion relative du réseau en fonction des proximités entre nœuds.
- **k-Plex** : Les k-plex révèlent des groupes denses avec quelques absences de liens, offrant une vision plus réaliste de la cohésion des réseaux où certains liens peuvent être absents.

Ces extensions des cliques permettent de détecter des structures denses dans les réseaux tout en prenant en compte des absences de connexion qui seraient fréquentes dans des contextes réels.
### 2.2. Méthodes Basées sur les Blocs (Moody & White, 2003)

Les **blocs cohésifs** (ou "cohesive blocks") sont des sous-structures dans un réseau social caractérisées par une cohésion interne particulièrement forte, mesurée par le degré de connectivité entre les nœuds du bloc. Cette approche repose sur l’idée que les sous-ensembles cohésifs d'un réseau révèlent les groupes de nœuds entre lesquels les liens sont suffisamment nombreux et redondants pour former des groupes relativement "résistants" et unis. 

Le concept est particulièrement utile pour identifier des noyaux denses au sein d'un réseau, qui peuvent représenter des groupes fortement soudés, tels que des équipes de travail, des alliances ou des sous-groupes d’amis partageant des intérêts communs.

**Notions Fondamentales des Blocs Cohésifs**

Les blocs cohésifs sont définis par des niveaux successifs de connectivité :
- **Connectivité k** : Un bloc cohésif de niveau \(k\) est un sous-ensemble dans lequel chaque paire de nœuds est reliée par au moins \(k\) chemins disjoints. Cela signifie que pour "couper" toutes les connexions entre deux nœuds dans un bloc de niveau \(k\), il faut supprimer au moins \(k\) nœuds du bloc, ce qui démontre la redondance et la résilience de ces connexions.
- **Hiérarchie des blocs** : Dans un réseau, les blocs peuvent être hiérarchisés par niveaux de cohésion croissants. Les blocs de niveau 1 contiennent les connexions les plus basiques, alors que ceux de niveau \(k\) (par exemple, \(k = 3\) ou \(k = 4\)) sont de plus en plus cohésifs et résistants, donc plus petits et plus denses.

**Détection des Blocs Cohésifs en R**

Le code ci-dessous montre comment détecter les blocs cohésifs dans un réseau avec le package `igraph`. La procédure consiste à convertir le réseau en graphe non orienté pour uniformiser les relations entre nœuds, puis à appliquer une fonction pour identifier les blocs cohésifs. Le résultat est un ensemble de sous-groupes fortement connectés, hiérarchisés par leur niveau de cohésion.

**Exemple de Code : Détection des Blocs Cohésifs**

```R
# Conversion du graphe en non-orienté
net_sym <- as.undirected(net, mode = "collapse", edge.attr.comb = list(Weight = "sum", "ignore"))

# Détection des blocs cohésifs dans le réseau
netblocks <- cohesive_blocks(net_sym)

# Résumé des blocs détectés
summary(netblocks)

# Obtenir le nombre total de blocs détectés
num_blocks <- length(netblocks$blocks)
cat("Nombre de blocs cohésifs détectés :", num_blocks, "\n")

# Affichage des membres de chaque bloc
blocks_list <- blocks(netblocks)
print(blocks_list)

# Visualisation des blocs cohésifs
plot(netblocks, net_sym, vertex.size = 5, vertex.label = NA, main = "Blocs Cohésifs du Réseau")
```

**Interprétation des Résultats**

Après avoir exécuté le code ci-dessus, nous obtenons des informations clés sur la structure des blocs dans le réseau.

- **Hiérarchie et Cohésion** : Les blocs cohésifs révèlent des sous-ensembles hiérarchisés dans le réseau. Les nœuds d’un même bloc sont reliés par de multiples chemins, ce qui les rend plus résilients et interconnectés. Les blocs de niveau plus élevé (par exemple, blocs de niveau 3 ou plus) sont plus petits mais beaucoup plus cohésifs que les blocs de niveau inférieur.
- **Implications pour les Groupes** : Les nœuds au sein d’un même bloc cohésif ont une grande probabilité d'interagir de manière coordonnée et d'influencer leurs pairs plus fortement que des nœuds extérieurs à ce bloc. Cela peut indiquer la présence de groupes soudés dans des réseaux sociaux, où des individus partagent des intérêts communs, collaborent étroitement ou échangent des informations de manière fréquente.
- **Structure Hierarchique** : Le fait que les blocs soient organisés par niveau de connectivité montre aussi la robustesse et la structure de redondance du réseau. Plus un bloc est "profond" dans la hiérarchie de cohésion, plus il est résistant aux perturbations, et plus les connexions sont multiples entre ses membres.

Les blocs cohésifs fournissent donc une vue approfondie de la structure organisationnelle du réseau en révélant des sous-groupes fortement interconnectés et hiérarchisés selon leur cohésion interne. Ils permettent ainsi d’explorer non seulement l’appartenance des nœuds à des groupes denses, mais aussi la hiérarchie et la résilience de ces groupes.

### 2.3. Méthodes Basées sur les k-Cores

La détection des **k-cores** dans un réseau permet de repérer des sous-ensembles de nœuds dont chaque membre est connecté à au moins \( k \) autres membres du groupe. Cela met en avant des **noyaux denses et cohésifs** où les relations sont suffisamment nombreuses pour résister à la perte de quelques liens sans que le sous-groupe se désagrège. 

Un k-core est donc un sous-graphe qui satisfait le critère de connectivité minimale de \( k \). Par exemple :
- Dans un 3-core, chaque nœud est connecté à au moins trois autres nœuds dans ce sous-ensemble.
- Cette contrainte rend la structure des k-cores rigide, car chaque nœud doit maintenir un niveau de connectivité minimum. 

Les k-cores sont particulièrement utiles pour :
- **Identifier les noyaux denses** de réseaux sociaux ou de collaborations scientifiques.
- **Analyser la robustesse des réseaux**, car les k-cores mettent en évidence les parties du réseau les plus résistantes à la perte de connexions.

**Calcul du k-Core et Visualisation**

En R, la fonction `coreness()` du package `igraph` permet d’attribuer à chaque nœud une valeur de coreness correspondant au k-core auquel il appartient. Ainsi, un nœud avec un **coreness de 3** fait partie d’un 3-core, mais pas nécessairement d’un 4-core.

```R
# Calculer le coreness de chaque nœud
V(net)$coreness <- coreness(net, mode = "all")

# Visualisation des k-cores
plot(net, vertex.size = V(net)$coreness * 3, 
     vertex.label = NA, 
     vertex.color = V(net)$coreness, 
     main = "k-Cores du Réseau")
```

Interprétation des k-Cores

- **Centralité et Cohésion** : Les nœuds ayant un **coreness élevé** (par exemple, 4 ou plus) occupent une position centrale dans les zones les plus denses du réseau. Ce sont souvent des éléments de cohésion majeurs.
- **Niveaux de Coreness** : En visualisant les valeurs de coreness, on peut voir des **groupes concentriques**, où les nœuds avec des coreness plus élevés sont nichés à l’intérieur des zones de coreness plus faibles, formant des couches de densité croissante vers le centre du réseau.

**Comparaison avec d’autres méthodes de détection de communautés**

Les k-cores se distinguent des blocs cohésifs ou des k-plex par leur rigidité dans la connectivité. Là où :
- **Les k-plex** tolèrent quelques connexions manquantes, permettant une certaine flexibilité.
- **Les blocs cohésifs** identifient les groupes denses sans contrainte minimale sur chaque connexion individuelle.
  
Les k-cores, quant à eux, exigent que chaque membre d’un k-core maintienne une relation avec un nombre minimum d’autres membres, ce qui peut représenter des groupes à forte stabilité structurelle.


## 3. Algorithmes Avancés de Détection de Communautés

Nous allons maintenant explorer les algorithmes les plus performants pour la détection de communautés, en optimisant le code et en gérant les paramètres pour obtenir les meilleurs résultats.

### 3.1. Algorithme de Louvain (Blondel et al., 2008)

- Méthode heuristique pour maximiser la **modularité**.
- Fonctionne en deux phases :
  - **Attribution locale** : Chaque nœud est assigné à la communauté qui maximise l'augmentation de la modularité.
  - **Agrégation** : Les communautés sont agrégées en super-nœuds, et le processus est répété.

**Gestion Optimale des Paramètres**

- **Poids des arêtes** : Utiliser les poids si disponibles pour une détection plus précise.
- **Résolution** : Ajuster pour détecter des communautés plus petites ou plus grandes (non disponible directement dans l'implémentation standard de Louvain).

**Application Optimisée en R avec l'Algorithme Leiden**

L'algorithme de **Leiden** est une amélioration de l'algorithme de Louvain, offrant de meilleures performances et une meilleure qualité des communautés détectées.

```R
# Installer et charger le package 'leidenAlg' si nécessaire
if (!requireNamespace("leidenAlg", quietly = TRUE)) {
    install.packages("leidenAlg")
}
library(leidenAlg)

# Détection des communautés avec Leiden
partition_leiden <- leiden(net_sym, weights = E(net_sym)$Weight, resolution_parameter = 1.0, n_iterations = -1)

# Assignation des communautés aux nœuds
V(net_sym)$community_leiden <- as.numeric(membership(partition_leiden))

# Calcul de la modularité
modularity_leiden <- modularity(net_sym, V(net_sym)$community_leiden, weights = E(net_sym)$Weight)
cat("Modularité (Leiden) :", modularity_leiden, "\n")

# Nombre de communautés
num_communities_leiden <- length(unique(V(net_sym)$community_leiden))
cat("Nombre de communautés détectées (Leiden) :", num_communities_leiden, "\n")
```

**Explication des Paramètres**
	1. **`graph`** : Le graphe `igraph` sur lequel vous souhaitez appliquer l'algorithme de Leiden. Ce graphe doit être non orienté. Il peut être pondéré si des poids d’arêtes sont fournis.
	2. **`objective_function`** : La fonction objective à optimiser pour détecter les communautés.
	    - `"modularity"` : Optimise la modularité standard, qui évalue la densité des liens internes par rapport à des liens aléatoires.
	    - `"CPM"` (Constant Potts Model) : Optimise la partition en utilisant un modèle alternatif, idéal pour des résolutions élevées où les communautés plus petites sont préférables.
	3. **`resolution_parameter`** : Définit le niveau de résolution de l’algorithme.
	    - Plus la résolution est élevée (>1), plus l’algorithme identifie de petites communautés.
	    - Une résolution plus faible (<1) regroupe les nœuds en de plus grandes communautés.
	    - La valeur par défaut est `1.0`, mais elle peut être ajustée en fonction des besoins de granularité de l’analyse.
	4. **`n_iterations`** : Nombre d’itérations de l’algorithme pour améliorer la partition.
	    - Par défaut, `-1` signifie que l’algorithme continuera jusqu’à ce qu’aucune amélioration ne soit possible.
	    - Vous pouvez spécifier un nombre fixe d'itérations pour limiter la durée de calcul sur les réseaux très grands.
	5. **`initial_membership`** : Un vecteur de partition initiale.
	    - Cela peut être utile si vous disposez d'une partition préexistante du réseau, et souhaitez simplement l’optimiser davantage avec Leiden.
	    - Par défaut, le réseau n’a aucune partition initiale.
	6. **`weights`** : Un vecteur pour indiquer les poids d’arêtes si le graphe est pondéré.
	    - En l'absence de spécification, les arêtes sont considérées comme ayant toutes le même poids.
	7. **`seed`** : Permet de spécifier une graine aléatoire pour garantir des résultats reproductibles.

**Optimisation des Paramètres**

- **Résolution** : Permet d'ajuster la taille des communautés.

```R
# Tester différentes valeurs de résolution
resolutions <- seq(0.5, 2.0, by = 0.1)
modularities <- numeric(length(resolutions))
num_communities <- numeric(length(resolutions))

for (i in seq_along(resolutions)) {
    res <- resolutions[i]
    partition <- leiden(net_sym, weights = E(net_sym)$Weight, resolution_parameter = res, n_iterations = -1)
    V(net_sym)$community_leiden <- as.numeric(membership(partition))
    modularities[i] <- modularity(net_sym, V(net_sym)$community_leiden, weights = E(net_sym)$Weight)
    num_communities[i] <- length(unique(V(net_sym)$community_leiden))
}

# Visualiser l'impact de la résolution sur la modularité et le nombre de communautés
par(mfrow = c(1, 2))
plot(resolutions, modularities, type = "b", col = "blue", xlab = "Résolution", ylab = "Modularité", main = "Impact de la Résolution sur la Modularité")
plot(resolutions, num_communities, type = "b", col = "red", xlab = "Résolution", ylab = "Nombre de Communautés", main = "Impact de la Résolution sur le Nombre de Communautés")
par(mfrow = c(1, 1))
```

**Interprétation** :

- Une résolution plus élevée tend à détecter des communautés plus petites.
- Choisir la résolution qui maximise la modularité tout en ayant un nombre raisonnable de communautés.

### 3.2. Algorithme Infomap (Rosvall & Bergstrom, 2008)

L'algorithme **Infomap** est un modèle de détection des communautés qui repose sur la **théorie de l'information** et utilise des **marches aléatoires** pour cartographier la structure des réseaux. L'idée centrale est que les communautés dans un réseau peuvent être considérées comme des zones où une marche aléatoire (par exemple, un flux d'information) a tendance à rester plus longtemps, en raison des connexions denses entre les nœuds de la communauté. Infomap utilise ce principe pour minimiser une mesure de code de description et obtenir une partition du réseau qui maximise la cohésion interne des communautés.

- **Approche théorique** : L'algorithme cherche à minimiser la longueur d'une description du flux d'information entre les nœuds, basée sur le principe que les marches aléatoires restent plus longtemps dans les communautés bien connectées.
- **Utilisation des poids** : Si les liens sont pondérés, l'algorithme peut aussi tenir compte de l'intensité des connexions, donnant ainsi plus de poids aux liens forts.

**Application Optimisée en R**

Voici comment appliquer l'algorithme Infomap en R avec le package `igraph` :

```R
# Détection des communautés avec Infomap, avec prise en compte des poids d’arêtes si disponibles
cinfomap <- cluster_infomap(net_sym, e.weights = E(net_sym)$Weight)

# Assignation des communautés détectées à chaque nœud
V(net_sym)$community_infomap <- membership(cinfomap)

# Calcul de la modularité pour évaluer la qualité de la détection des communautés
modularity_infomap <- modularity(cinfomap)
cat("Modularité (Infomap) :", modularity_infomap, "\n")

# Nombre de communautés détectées
num_communities_infomap <- length(cinfomap)
cat("Nombre de communautés détectées (Infomap) :", num_communities_infomap, "\n")
```

**Interprétation des Résultats**

- **Modularité** : La valeur de modularité obtenue indique dans quelle mesure les communautés détectées sont cohésives. Une modularité plus élevée signifie que les nœuds à l'intérieur des communautés sont plus densément connectés que les liens entre les communautés. Dans le contexte d'Infomap, elle permet de vérifier que l'algorithme a détecté des partitions optimales.
- **Nombre de Communautés** : Un nombre plus élevé de communautés suggère une structure plus divisée du réseau, avec plusieurs sous-groupes denses.

**Optimisation des Paramètres de l'Algorithme Infomap**

- **Poids des arêtes (`e.weights`)** : Dans les réseaux pondérés, spécifiez `e.weights = E(net_sym)$Weight` pour indiquer l’intensité des liens. Cela permet à l'algorithme de prioriser les liens forts lors de la détection des communautés, renforçant ainsi les partitions.
- **Nombre de Réplications** : Bien qu'Infomap dans `igraph` n'ait pas de paramètre explicite pour les réplicas, certains réglages peuvent être faits pour affiner les résultats en modifiant le graphe d'entrée, par exemple en renforçant les poids des arêtes ou en ajustant les connexions.

**Visualisation et Analyse des Communautés Infomap**

La visualisation des communautés peut être utile pour interpréter les résultats et observer la structure des communautés détectées.

```R
# Visualisation des communautés avec les couleurs correspondant aux groupes Infomap
plot(
  net_sym, 
  vertex.color = V(net_sym)$community_infomap, 
  vertex.size = 5, 
  vertex.label = NA, 
  main = "Communautés détectées avec l'algorithme Infomap"
)
```

**Interprétation des Communautés Infomap**

- **Communautés Cohésives** : Les communautés détectées par Infomap représentent des groupes où les échanges internes sont plus probables. Cela en fait une méthode particulièrement efficace pour identifier des clusters dans des réseaux où les interactions sont intenses au sein des groupes mais limitées entre eux.
- **Applications Pratiques** : Infomap est particulièrement adapté pour les réseaux sociaux, les réseaux de communication, ou toute situation où les flux d’information ou d'influence sont une caractéristique clé du réseau. Par exemple, il peut identifier des groupes d'influenceurs dans les réseaux sociaux ou des groupes de sites interconnectés dans des réseaux de citations académiques.

En résumé, l'algorithme Infomap se base sur la minimisation d'un code de description et utilise des marches aléatoires pour identifier les structures de communautés dans un réseau, offrant une alternative efficace à l’algorithme de Louvain pour des réseaux où les flux d’information sont significatifs.

### 3.3. Algorithme Walktrap (Pons & Latapy, 2005)

L’algorithme **Walktrap** est basé sur des **marches aléatoires** pour détecter des communautés au sein des réseaux. Son principe repose sur l'idée que les nœuds qui appartiennent à la même communauté seront souvent visités ensemble lors d’une marche aléatoire, car ils sont densément connectés. En d’autres termes, la marche aléatoire a une probabilité plus élevée de rester dans une communauté bien connectée avant de passer à une autre, ce qui permet de regrouper ces nœuds en communautés cohésives.

- **Utilisation des marches aléatoires** : Cet algorithme utilise la distance aléatoire entre les nœuds, mesurant à quel point ils sont proches dans un contexte de marche aléatoire.
- **Ajustement des paramètres** : Le nombre de pas des marches aléatoires peut être ajusté pour capturer les communautés avec un niveau de détail différent.

**Application Optimisée en R**

Voici comment appliquer l’algorithme Walktrap en R avec le package `igraph` :

```R
# Détection des communautés avec Walktrap
cwalktrap <- cluster_walktrap(net_sym, weights = E(net_sym)$Weight, steps = 4)

# Assignation des communautés détectées à chaque nœud
V(net_sym)$community_walktrap <- membership(cwalktrap)

# Calcul de la modularité pour évaluer la qualité de la partition en communautés
modularity_walktrap <- modularity(cwalktrap)
cat("Modularité (Walktrap) :", modularity_walktrap, "\n")

# Nombre de communautés détectées
num_communities_walktrap <- length(cwalktrap)
cat("Nombre de communautés détectées (Walktrap) :", num_communities_walktrap, "\n")
```

**Interprétation des Résultats**

- **Modularité** : Comme pour d’autres algorithmes de détection de communautés, la modularité obtenue avec Walktrap mesure la densité des liens au sein des communautés par rapport à ce qu’on attendrait si les liens étaient distribués aléatoirement. Une modularité plus élevée indique une meilleure séparation des communautés.
- **Nombre de Communautés** : Le nombre de communautés détectées permet de voir combien de sous-groupes cohésifs existent dans le réseau.

**Optimisation des Paramètres de l'Algorithme Walktrap**

- **Nombre de Pas (`steps`)** : Le paramètre `steps` indique combien de pas la marche aléatoire doit effectuer avant de calculer les distances entre nœuds. Un nombre de pas plus élevé permet à la marche aléatoire d'explorer davantage le réseau, capturant ainsi des communautés de plus grande taille. Par défaut, `steps = 4` est souvent utilisé, mais vous pouvez ajuster ce paramètre pour optimiser la détection des communautés dans les réseaux avec des structures plus ou moins denses.

**Visualisation et Analyse des Communautés Walktrap**

Une visualisation peut aider à interpréter la structure des communautés détectées par Walktrap :

```R
# Visualisation des communautés avec les couleurs correspondant aux groupes Walktrap
plot(
  net_sym, 
  vertex.color = V(net_sym)$community_walktrap, 
  vertex.size = 5, 
  vertex.label = NA, 
  main = "Communautés détectées avec l'algorithme Walktrap"
)
```

**Interprétation des Communautés Walktrap**

- **Communautés denses et proches** : Les communautés détectées avec Walktrap regroupent les nœuds qui sont fréquemment connectés et proches dans les marches aléatoires, révélant des groupes cohésifs dans le réseau.
- **Applications Pratiques** : Walktrap est utile dans des contextes où la connectivité entre les nœuds est dense au sein des communautés mais s’affaiblit entre elles, comme dans les réseaux sociaux, où il peut identifier des groupes d’intérêts ou de proximité.

En résumé, l'algorithme Walktrap est une méthode de détection de communautés efficace, notamment pour les réseaux où la proximité aléatoire entre nœuds dans des marches aléatoires peut refléter des structures communautaires sous-jacentes.
### 3.4. Comparaison des Algorithmes de Détection de Communautés

Pour évaluer l'efficacité et les différences entre les algorithmes, nous collectons des résultats relatifs à des métriques clés telles que la modularité et le nombre de communautés. Cette comparaison permet de mieux comprendre quel algorithme s'adapte le mieux à la structure particulière du réseau.

**Collecte des Résultats**

La collecte des résultats se fait en rassemblant les valeurs de modularité et le nombre de communautés détectées pour chaque algorithme dans un tableau de comparaison.

```R
# Créer un tableau récapitulatif des résultats pour chaque algorithme
results <- data.frame(
    Algorithme = c("Leiden", "Infomap", "Walktrap"),
    Modularité = c(modularity_leiden, modularity_infomap, modularity_walktrap),
    Nombre_Communautés = c(num_communities_leiden, num_communities_infomap, num_communities_walktrap)
)

# Afficher le tableau récapitulatif
print(results)
```

**Interprétation des Résultats**

Les résultats fournis par le tableau permettent d'analyser les différences et les points forts de chaque algorithme.

- **Modularité** : La valeur de modularité indique dans quelle mesure les communautés sont bien séparées par rapport à un modèle aléatoire. Une valeur de modularité plus élevée indique une meilleure séparation des communautés, ce qui signifie que les liens sont plus concentrés à l'intérieur des communautés par rapport à l'extérieur. L'algorithme avec la modularité la plus élevée est souvent considéré comme le plus performant pour ce réseau spécifique.
  
- **Nombre de Communautés** : Un bon algorithme doit trouver un équilibre en termes de nombre de communautés. Un nombre de communautés trop élevé peut fragmenter le réseau, tandis qu’un nombre trop faible peut manquer de détails sur la structure communautaire. Il est donc crucial de regarder le nombre de communautés pour chaque algorithme et d’évaluer sa pertinence en fonction de la modularité.
### Conclusion

Cette comparaison des algorithmes met en lumière l'importance de choisir la méthode en fonction des caractéristiques spécifiques du réseau. En ajustant les paramètres et en interprétant les résultats de manière critique, les chercheurs peuvent identifier les algorithmes qui fournissent les meilleures informations sur la structure communautaire du réseau.
### Références

- **Blondel, V. D., Guillaume, J.-L., Lambiotte, R., & Lefebvre, E. (2008).** Fast unfolding of communities in large networks. *Journal of Statistical Mechanics: Theory and Experiment*, 2008(10), P10008.
- **Traag, V. A., Waltman, L., & van Eck, N. J. (2019).** From Louvain to Leiden: guaranteeing well-connected communities. *Scientific Reports*, 9(1), 5233.
- **Rosvall, M., & Bergstrom, C. T. (2008).** Maps of random walks on complex networks reveal community structure. *Proceedings of the National Academy of Sciences*, 105(4), 1118–1123.
- **Pons, P., & Latapy, M. (2005).** Computing communities in large networks using random walks. *International Symposium on Computer and Information Sciences*, 284–293.


# A voir

## Modèles de Structure Latente

## Mixed Membership Stochastic Block Models (MMSBM)

Développés par Airoldi et al. (2008), les MMSBM représentent une avancée significative dans la modélisation des communautés superposées[

3

](https://arxiv.org/abs/2307.14530). Leurs caractéristiques incluent:

- La possibilité pour les nœuds d'appartenir à plusieurs communautés
- L'analyse des structures de communautés chevauchantes
- L'estimation optimale des relations entre communautés

## Modèles d'Espace Latent (LSM)

Les LSM et leurs extensions dynamiques (DLSM) permettent de

1

:

- Capturer les similarités implicites entre nœuds
- Projeter les relations dans un espace latent
- Observer l'évolution des proximités temporelles