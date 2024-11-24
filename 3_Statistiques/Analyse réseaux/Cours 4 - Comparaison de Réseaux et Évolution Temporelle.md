Dans ce cours, nous allons explorer les méthodes et les paramètres utilisés pour comparer différents réseaux, ainsi que les techniques d'analyse longitudinale pour étudier l'évolution des réseaux au fil du temps. Comprendre comment les réseaux changent et évoluent est essentiel pour analyser les tendances relationnelles globales et pour prévoir les dynamiques futures dans divers contextes, tels que les réseaux sociaux en ligne, les réseaux de communication, ou les réseaux biologiques.

#### Objectifs du cours

- **Comprendre les paramètres clés pour comparer différents réseaux.**
- **Apprendre les méthodes d'analyse longitudinale pour étudier l'évolution des réseaux.**
- **Étudier les tendances relationnelles globales et leur impact sur la structure des réseaux.**
- **Acquérir des compétences pratiques en utilisant le langage R pour analyser et comparer des réseaux à différents moments dans le temps.**

### 1. Comparer Différents Réseaux ou sous-réseaux

Comparer des réseaux permet de comprendre comment des structures relationnelles diffèrent selon les contextes, les populations, ou les périodes temporelles. Les comparaisons peuvent révéler des similitudes, des différences structurelles, et des tendances qui ne sont pas évidentes en examinant un seul réseau isolément.

#### Paramètres Clés pour la Comparaison

**Taille du Réseau**

- **Nombre de nœuds (N)** : Indique la taille du réseau en termes de nombre d'entités.
- **Nombre de liens (E)** : Indique la densité potentielle du réseau.
- **Densité du Réseau** : La densité mesure la proportion des liens existants par rapport au nombre maximum de liens possibles.
- **Degré Moyen** : Moyenne des degrés des nœuds du réseau.
- **Distribution des Degrés** : La forme de la distribution (loi de puissance, loi normale, etc.) peut différer entre les réseaux.

**Densité des réseaux**

- **Coefficient de Clustering**
- **Diamètre** : Distance géodésique maximale dans le réseau.
- **Distance Moyenne** : Distance moyenne entre tous les paires de nœuds.

**Communautarisme**
- **Coefficient d'assortativité** : Peut être comparé entre réseaux pour comprendre les tendances de connexion.
- **Modularity** : Mesure la force de division d'un réseau en communautés.

#### Exemple Pratique en R

Supposons que nous ayons deux réseaux issus de contextes différents : `network1` et `network2`, représentés par leurs fichiers de liens `links1.txt` et `links2.txt`, et leurs fichiers de nœuds `nodes1.txt` et `nodes2.txt`.

**Calcul des Paramètres avec la fonction CompareNet**

```r

AnalyseNet <- function(net) {
  # Variables basiques
  v_count <- vcount(net)
  e_count <- ecount(net)
  
  # Taille et propriétés des noeuds
  node_sizes <- igraph::degree(net)
  node_sizes_in <- igraph::degree(net, mode = "in")
  node_sizes_out <- igraph::degree(net, mode = "out")
  edge_sizes <- E(net)$Weight
  
  # Calculs spécifiques
  triades <- triad_census(net)
  
  # Création du data.frame de résultats
  resultats <- data.frame(
    Nom_du_Graphe = deparse(substitute(net)),
    Nombre_de_Noeuds = v_count,
    Nombre_de_Liens = e_count,
    Moyenne_Degre = mean(node_sizes),
    Median_Degre = median(node_sizes),
    SD_Degre = sd(node_sizes),
    Min_Degre = min(node_sizes),
    Max_Degre = max(node_sizes),
    Moyenne_Degre_In = mean(node_sizes_in),
    Median_Degre_In = median(node_sizes_in),
    SD_Degre_In = sd(node_sizes_in),
    Min_Degre_In = min(node_sizes_in),
    Max_Degre_In = max(node_sizes_in),
    Moyenne_Degre_Out = mean(node_sizes_out),
    Median_Degre_Out = median(node_sizes_out),
    SD_Degre_Out = sd(node_sizes_out),
    Min_Degre_Out = min(node_sizes_out),
    Max_Degre_Out = max(node_sizes_out),
    Moyenne_Poids_Liens = mean(edge_sizes),
    Median_Poids_Liens = median(edge_sizes),
    SD_Poids_Liens = sd(edge_sizes),
    Min_Poids_Liens = min(edge_sizes),
    Max_Poids_Liens = max(edge_sizes),
    Diametre = diameter(net, directed = TRUE, weights = E(net)$Weight),
    average_path_length = mean_distance(net, directed = TRUE),
    Longueur_Moyenne_Chemins = mean_distance(net, directed = TRUE, weights = E(net)$Weight),
    Rayon = min(eccentricity(net)),
    Assortativite_degree = assortativity_degree(net, directed = TRUE), 
    Transitivite = transitivity(net, type = "global"),
    Transitivite_mean = transitivity(net, type = "average"),
    Densite_edge = edge_density(net),
    Connexite_Forte = is_connected(net, mode = "strong"),
    Connexite_Faible = is_connected(net, mode = "weak"),
    Reciprocite = reciprocity(net),
    Mutual_Dyads = dyad_census(net)$mut,
    Asymmetric_Dyads = dyad_census(net)$asym,
    Null_Dyads = dyad_census(net)$null,
    # Ajouter chaque type de triade comme une colonne
    Triades_003 = triades[1],
    Triades_012 = triades[2],
    Triades_102 = triades[3],
    Triades_021D = triades[4],
    Triades_021U = triades[5],
    Triades_021C = triades[6],
    Triades_111D = triades[7],
    Triades_111U = triades[8],
    Triades_030T = triades[9],
    Triades_030C = triades[10],
    Triades_201 = triades[11],
    Triades_120D = triades[12],
    Triades_120U = triades[13],
    Triades_120C = triades[14],
    Triades_210 = triades[15],
    Triades_300 = triades[16]
    
  )
  
  return(resultats)
}
data_reseau <- AnalyseNet(net)
```

**Chargement des Réseaux sous-réseaux**

```R

CompareNet <- function(net, groups) {
    # Vérifiez que la variable 'groups' existe dans le graphe
    if (!(groups %in% vertex_attr_names(net))) {
        stop("La variable '", groups, "' n'existe pas dans le graphe.")
    }
    
    # Obtenez les modalités uniques de la variable 'groups' (en excluant "NA")
    modalites <- unique(vertex_attr(net, groups))
    modalites <- modalites[!is.na(modalites)]
    
    # Nettoyez les noms de modalités
    modalites_clean <- make.names(modalites, unique = TRUE)
    
    # Créez une liste pour stocker les résultats de chaque sous-graphe
    resultats_list <- list()
    
    # Boucle sur chaque modalité (en excluant "NA")
    for (i in seq_along(modalites)) {
      modalite <- modalites[i]
      modalite_clean <- modalites_clean[i]
        
      # Exclure les sommets avec des valeurs NA pour l'attribut 'groups'
      node_indices <- which(vertex_attr(net, groups) == modalite & !is.na(vertex_attr(net, groups)))
      if (length(node_indices) > 0) {
        node_indices <- node_indices[!is.na(node_indices)]
        node_indices <- match(node_indices, V(net)$name)
        node_indices <- node_indices[!is.na(node_indices)]
        sous_graphe <- induced_subgraph(net, node_indices)
        
        # Variables basiques
        v_count <- vcount(sous_graphe)
        e_count <- ecount(sous_graphe)
        
        # Taille et propriétés des noeuds
        node_sizes <- igraph::degree(sous_graphe)
        node_sizes_in <- igraph::degree(sous_graphe, mode = "in")
        node_sizes_out <- igraph::degree(sous_graphe, mode = "out")
        edge_sizes <- E(sous_graphe)$Weight
        
        # Calculs spécifiques
        triades <- triad_census(sous_graphe)
        
        # Création du data.frame de résultats pour le sous-graphe
        resultats <- data.frame(
            Nom_du_Graphe = paste0("net_", groups, "_", modalite_clean),
            Nombre_de_Noeuds = v_count,
            Nombre_de_Liens = e_count,
            Moyenne_Degre = mean(node_sizes),
            Median_Degre = median(node_sizes),
            SD_Degre = sd(node_sizes),
            Min_Degre = min(node_sizes),
            Max_Degre = max(node_sizes),
            Moyenne_Degre_In = mean(node_sizes_in),
            Median_Degre_In = median(node_sizes_in),
            SD_Degre_In = sd(node_sizes_in),
            Min_Degre_In = min(node_sizes_in),
            Max_Degre_In = max(node_sizes_in),
            Moyenne_Degre_Out = mean(node_sizes_out),
            Median_Degre_Out = median(node_sizes_out),
            SD_Degre_Out = sd(node_sizes_out),
            Min_Degre_Out = min(node_sizes_out),
            Max_Degre_Out = max(node_sizes_out),
            Moyenne_Poids_Liens = ifelse(length(edge_sizes) > 0, mean(edge_sizes), NA),
            Median_Poids_Liens = ifelse(length(edge_sizes) > 0, median(edge_sizes), NA),
            SD_Poids_Liens = ifelse(length(edge_sizes) > 0, sd(edge_sizes), NA),
            Min_Poids_Liens = ifelse(length(edge_sizes) > 0, min(edge_sizes), NA),
            Max_Poids_Liens = ifelse(length(edge_sizes) > 0, max(edge_sizes), NA),
            Diametre = diameter(sous_graphe, directed = TRUE, weights = E(sous_graphe)$Weight),
            average_path_length = mean_distance(sous_graphe, directed = TRUE),
            Longueur_Moyenne_Chemins = mean_distance(sous_graphe, directed = TRUE, weights = E(sous_graphe)$Weight),
            Rayon = min(eccentricity(sous_graphe)),
            Assortativite_degree = assortativity_degree(sous_graphe, directed = TRUE),
            Transitivite = transitivity(sous_graphe, type = "global"),
            Transitivite_mean = transitivity(sous_graphe, type = "average"),
            Densite_edge = edge_density(sous_graphe),
            Connexite_Forte = is_connected(sous_graphe, mode = "strong"),
            Connexite_Faible = is_connected(sous_graphe, mode = "weak"),
            Reciprocite = reciprocity(sous_graphe),
            Mutual_Dyads = dyad_census(sous_graphe)$mut,
            Asymmetric_Dyads = dyad_census(sous_graphe)$asym,
            Null_Dyads = dyad_census(sous_graphe)$null,
            Triades_003 = triades[1],
            Triades_012 = triades[2],
            Triades_102 = triades[3],
            Triades_021D = triades[4],
            Triades_021U = triades[5],
            Triades_021C = triades[6],
            Triades_111D = triades[7],
            Triades_111U = triades[8],
            Triades_030T = triades[9],
            Triades_030C = triades[10],
            Triades_201 = triades[11],
            Triades_120D = triades[12],
            Triades_120U = triades[13],
            Triades_120C = triades[14],
            Triades_210 = triades[15],
            Triades_300 = triades[16]
        )
        
        # Ajoutez les résultats du sous-graphe à la liste
        resultats_list[[paste0("net_", groups, "_", modalite_clean)]] <- resultats

       } else {
         warning("Le sous-graphe pour la modalité '", modalite, "' est vide. Passage à la modalité suivante.")
         next
       }
    }

    # Combine les résultats de tous les sous-graphes en un seul data.frame
    resultats_final <- do.call(rbind, resultats_list)
    
    return(resultats_final)
}


data_reseau_Politique <- CompareNet(net, "Politique")
data_reseau <- rbind(data_reseau, data_reseau_groups)
row.names(data_reseau) <- 1:nrow(data_reseau)
data_reseau

```

#### Visualisation des Résultats

Pour une meilleure interprétation, vous pouvez visualiser les résultats sous forme de tableau ou de graphique.

```r
# Installer le package reshape2 si nécessaire
# install.packages("reshape2")
library(reshape2)

# Transformation des données pour ggplot2
results_melted <- melt(results_df, id.vars = "Name")

# Installer le package ggplot2 si nécessaire
# install.packages("ggplot2")
library(ggplot2)

# Exemple de visualisation : comparaison des densités
ggplot(results_melted[results_melted$variable == "Density", ], aes(x = Name, y = value, fill = Name)) +
  geom_bar(stat = "identity") +
  labs(title = "Comparaison des densités des réseaux", x = "Réseau", y = "Densité") +
  theme_minimal()

```
#### Conclusion

**Interprétation**

- **Taille du Réseau** : Comparer les tailles pour voir si les différences structurelles sont liées à la taille.
- **Densité** : Un réseau plus dense peut indiquer une interaction plus fréquente ou un environnement plus collaboratif.
- **Degré Moyen** : Peut refléter le niveau moyen de connectivité des nœuds.
- **Clustering** : Un clustering plus élevé suggère une plus grande tendance à former des groupes ou communautés.
- **Diamètre et Distance Moyenne** : Indiquent à quel point le réseau est étendu en termes de chemins.
- **Assortativité** : Un coefficient positif indique que les nœuds ont tendance à se connecter à des nœuds de degré similaire.
- **Modularity** : Une modularité plus élevée indique une structure communautaire plus prononcée.

---

### 2. Analyse Longitudinale de l'Évolution des Réseaux

L'analyse longitudinale consiste à étudier les changements dans un réseau au fil du temps. Cela permet de comprendre comment les structures relationnelles évoluent, comment de nouveaux liens se forment, comment certains liens disparaissent, et quelles sont les tendances globales de l'évolution du réseau.

**Méthodes**

- **Snapshots** : Obtenir des "photos" du réseau à différents moments (par exemple, mensuellement, annuellement).
- **Données Longitudinales** : Données qui suivent les mêmes nœuds sur plusieurs périodes.

**Mesures Dynamiques**

- **Formation et Dissolution des Liens** : Étudier quels liens sont créés ou supprimés entre les périodes.
- **Changements de Degré** : Suivre l'évolution du degré des nœuds individuels.
- **Évolution des Communautés** : Observer comment les communautés se forment, se fusionnent ou se divisent au fil du temps.
- **Centralité Temporelle** : Analyser comment les mesures de centralité des nœuds évoluent.

**Réseau à un temps t1, t2 et t3**

Supposons que nous ayons des données pour un réseau à trois moments dans le temps : `t1`, `t2`, et `t3`.


```R
library(readr) 
library(lubridate) 
library(igraph)

graphcut <- function(links, step = NULL, startdate = NULL, enddate = NULL) {
    # Vérification si le package igraph est installé
    if (!requireNamespace("igraph", quietly = TRUE)) {
        # Demander à l'utilisateur s'il souhaite installer igraph
        response <- readline(prompt = "Le package 'igraph' n'est pas installé. Voulez-vous l'installer maintenant ? (O/N) : ")
        if (toupper(response) == "O" || toupper(response) == "OUI") {
            install.packages("igraph")
        } else {
            stop("Le package 'igraph' est nécessaire pour exécuter cette fonction.")
        }
    }
    # Chargement du package igraph
    if (!("package:igraph" %in% search())) {
        library(igraph)
    }

    # Si 'links' est un chemin de fichier, le charger
    if (is.character(links)) {
        if (file.exists(links)) {
            links <- read.csv(links, header = TRUE, stringsAsFactors = FALSE)
        } else {
            stop("Le fichier spécifié dans 'links' n'existe pas.")
        }
    } else if (!is.data.frame(links)) {
        stop("'links' doit être un dataframe ou un chemin vers un fichier CSV.")
    }

    # Conversion de 'publishedat' en objet Date
    if (!("publishedat" %in% names(links))) {
        stop("La colonne 'publishedat' est manquante dans les données 'links'.")
    }
    links$publishedat <- as.Date(links$publishedat, format = "%d/%m/%Y")

    # Vérification des dates non converties (NA)
    if (any(is.na(links$publishedat))) {
        warning("Certaines dates dans 'publishedat' n'ont pas pu être converties et sont NA.")
    }

    # Si startdate ou enddate sont NULL, prendre les dates min et max
    if (is.null(startdate)) {
        startdate <- min(links$publishedat, na.rm = TRUE)
    } else {
        startdate <- as.Date(startdate)
    }
    if (is.null(enddate)) {
        enddate <- max(links$publishedat, na.rm = TRUE)
    } else {
        enddate <- as.Date(enddate)
    }

    # Filtrer les liens entre startdate et enddate
    links_filtered <- subset(links, publishedat >= startdate & publishedat <= enddate)

    if (is.null(step)) {
        # Pas de découpage, créer un seul graphe
        g <- graph_from_data_frame(d = links_filtered[, c("source", "target")], directed = FALSE)
        return(g)
    } else if (step == "year" || step == "month") {
        # Ajouter les colonnes 'year' et 'year_month' pour le découpage
        links_filtered$year <- format(links_filtered$publishedat, "%Y")
        links_filtered$year_month <- format(links_filtered$publishedat, "%Y-%m")

        # Créer une liste des périodes
        if (step == "year") {
            periods <- sort(unique(links_filtered$year))
            links_by_period <- split(links_filtered, links_filtered$year)
        } else if (step == "month") {
            periods <- sort(unique(links_filtered$year_month))
            links_by_period <- split(links_filtered, links_filtered$year_month)
        }

        # Créer les graphes pour chaque période
        graphs_by_period <- list()
        for (period in periods) {
            df <- links_by_period[[period]]
            g <- graph_from_data_frame(d = df[, c("source", "target")], directed = FALSE)
            graphs_by_period[[period]] <- g
        }
        return(graphs_by_period)
    } else {
        stop("Le paramètre 'step' doit être NULL, 'month' ou 'year'.")
    }
}



```

#### 2.1. Calcul du Nombre de Nœuds et de Liens par Période

**Pour les Années**

```R
# Initialiser un dataframe pour stocker les résultats
network_evolution_year <- data.frame(
    Year = character(),
    Nodes = integer(),
    Edges = integer(),
    Density = numeric(),
    stringsAsFactors = FALSE
)

# Parcourir les graphes annuels et calculer les métriques
for (year in names(graphs_by_year)) {
    g <- graphs_by_year[[year]]
    N <- vcount(g)
    E <- ecount(g)
    density <- edge_density(g)
    
    # Ajouter les résultats au dataframe
    network_evolution_year <- rbind(network_evolution_year, data.frame(
        Year = year,
        Nodes = N,
        Edges = E,
        Density = density,
        stringsAsFactors = FALSE
    ))
}
```

**Pour les Mois**

```R
# Initialiser un dataframe pour les résultats mensuels
network_evolution_month <- data.frame(
    Year_Month = character(),
    Nodes = integer(),
    Edges = integer(),
    Density = numeric(),
    stringsAsFactors = FALSE
)

# Parcourir les graphes mensuels et calculer les métriques
for (ym in names(graphs_by_month)) {
    g <- graphs_by_month[[ym]]
    N <- vcount(g)
    E <- ecount(g)
    density <- edge_density(g)
    
    # Ajouter les résultats au dataframe
    network_evolution_month <- rbind(network_evolution_month, data.frame(
        Year_Month = ym,
        Nodes = N,
        Edges = E,
        Density = density,
        stringsAsFactors = FALSE
    ))
}
```

#### 2.2. Visualisation de l'Évolution du Réseau

**Évolution Annuelle**

```R
# Installer ggplot2 si nécessaire
if (!requireNamespace("ggplot2", quietly = TRUE)) {
    install.packages("ggplot2")
}
library(ggplot2)

# Tracé du nombre de nœuds et de liens au fil des années
ggplot(network_evolution_year, aes(x = as.integer(Year))) +
    geom_line(aes(y = Nodes, color = "Nœuds")) +
    geom_line(aes(y = Edges, color = "Liens")) +
    labs(title = "Évolution du réseau par année", x = "Année", y = "Nombre") +
    scale_color_manual(name = "Légende", values = c("Nœuds" = "blue", "Liens" = "red")) +
    theme_minimal()
```

**Évolution Mensuelle**

```R
# Convertir Year_Month en format date pour l'axe x
network_evolution_month$Date <- as.Date(paste0(network_evolution_month$Year_Month, "-01"))

# Tracé du nombre de nœuds et de liens au fil des mois
ggplot(network_evolution_month, aes(x = Date)) +
    geom_line(aes(y = Nodes, color = "Nœuds")) +
    geom_line(aes(y = Edges, color = "Liens")) +
    labs(title = "Évolution du réseau par mois", x = "Date", y = "Nombre") +
    scale_color_manual(name = "Légende", values = c("Nœuds" = "blue", "Liens" = "red")) +
    theme_minimal()
```

**Explication :**

- **Visualisation** : Ces graphiques permettent de visualiser comment le nombre de nœuds et de liens évolue au fil du temps.
- **Analyse** : On peut observer les tendances, comme une croissance, une stabilité ou une décroissance du réseau.
#### 2.3 Analyse des Changements de Liens

**Calcul des nouveaux liens et des liens dissous entre t1 et t2 :**

```R
# Sélection des périodes
periods <- sort(names(graphs_by_month))

# Initialiser un dataframe pour les changements
link_changes <- data.frame(
    Period = character(),
    New_Links = integer(),
    Dissolved_Links = integer(),
    stringsAsFactors = FALSE
)

# Parcourir les périodes consécutives
for (i in 2:length(periods)) {
    prev_period <- periods[i - 1]
    current_period <- periods[i]
    
    g_prev <- graphs_by_month[[prev_period]]
    g_curr <- graphs_by_month[[current_period]]
    
    # Extraire les liens sous forme de dataframes
    edges_prev <- as.data.frame(get.edgelist(g_prev))
    edges_curr <- as.data.frame(get.edgelist(g_curr))
    
    # Renommer les colonnes pour correspondre
    colnames(edges_prev) <- c("source", "target")
    colnames(edges_curr) <- c("source", "target")
    
    # Nouveaux liens : présents dans current_period mais pas dans prev_period
    new_links <- nrow(setdiff(edges_curr, edges_prev))
    
    # Liens dissous : présents dans prev_period mais pas dans current_period
    dissolved_links <- nrow(setdiff(edges_prev, edges_curr))
    
    # Ajouter les résultats au dataframe
    link_changes <- rbind(link_changes, data.frame(
        Period = current_period,
        New_Links = new_links,
        Dissolved_Links = dissolved_links,
        stringsAsFactors = FALSE
    ))
}
```

**Explication :**

- **`setdiff()`** : Identifie les lignes présentes dans un dataframe mais pas dans un autre.
- **Analyse des changements** : Permet de quantifier le nombre de nouveaux liens et de liens dissous entre chaque période.


#### 2.4 Extension de l'Analyse

Nous allons calculer les métriques suivantes pour chaque période (par mois dans cet exemple) :

- **Degré moyen (`Mean_Degree`)**
- **Coefficient de clustering moyen (`Clustering`)**
- **Diamètre du réseau (`Diameter`)**
- **Assortativité par degré (`Assortativity`)**
- **Modularité et nombre de communautés (`Modularity`, `Num_Communities`)**

**Mise à Jour du Dataframe `network_evolution_month`**

Ajoutons les nouvelles colonnes pour stocker les métriques :

```R
# Ajouter des colonnes pour les nouvelles métriques
network_evolution_month$Mean_Degree <- NA
network_evolution_month$Clustering <- NA
network_evolution_month$Diameter <- NA
network_evolution_month$Assortativity <- NA
network_evolution_month$Modularity <- NA
network_evolution_month$Num_Communities <- NA
```

Calcul des Métriques pour Chaque Période

```R
for (i in 1:nrow(network_evolution_month)) {
    ym <- network_evolution_month$Year_Month[i]
    g <- graphs_by_month[[ym]]
    
    # Vérifier si le graphe a des nœuds et des liens
    if (vcount(g) > 0 && ecount(g) > 0) {
        # Degré moyen
        degrees <- degree(g)
        mean_degree <- mean(degrees)
        
        # Coefficient de clustering moyen
        clustering <- transitivity(g, type = "average")
        
        # Diamètre du réseau
        diameter_value <- diameter(g)
        
        # Assortativité par degré
        assortativity_value <- assortativity_degree(g)
        
        # Détection des communautés
        communities <- cluster_louvain(g)
        modularity_value <- modularity(communities)
        num_communities <- length(communities)
    } else {
        # Si le graphe n'a pas de liens, définir les métriques à NA ou 0
        mean_degree <- 0
        clustering <- NA
        diameter_value <- NA
        assortativity_value <- NA
        modularity_value <- NA
        num_communities <- 0
    }
    
    # Enregistrer les métriques dans le dataframe
    network_evolution_month$Mean_Degree[i] <- mean_degree
    network_evolution_month$Clustering[i] <- clustering
    network_evolution_month$Diameter[i] <- diameter_value
    network_evolution_month$Assortativity[i] <- assortativity_value
    network_evolution_month$Modularity[i] <- modularity_value
    network_evolution_month$Num_Communities[i] <- num_communities
}
```

**Explications :**

- **Degré moyen (`Mean_Degree`)** : Moyenne des degrés des nœuds.
- **Coefficient de clustering moyen (`Clustering`)** : Mesure la tendance des nœuds à former des triangles.
- **Diamètre du réseau (`Diameter`)** : Plus longue distance minimale entre deux nœuds.
- **Assortativité par degré (`Assortativity`)** : Tendance des nœuds à se connecter à d'autres nœuds de degré similaire.
- **Modularité (`Modularity`)** : Qualité de la division du réseau en communautés.
- **Nombre de communautés (`Num_Communities`)** : Nombre total de communautés détectées.

**Visualisation des Métriques au Fil du Temps**

Évolution du Degré Moyen et du Clustering Moyen

```R
# Tracé du degré moyen
ggplot(network_evolution_month, aes(x = Date, y = Mean_Degree)) +
    geom_line(color = "blue") +
    labs(title = "Évolution du degré moyen par mois", x = "Date", y = "Degré moyen") +
    theme_minimal()

# Tracé du coefficient de clustering moyen
ggplot(network_evolution_month, aes(x = Date, y = Clustering)) +
    geom_line(color = "green") +
    labs(title = "Évolution du coefficient de clustering moyen par mois", x = "Date", y = "Clustering moyen") +
    theme_minimal()
```

Évolution du Diamètre et de l'Assortativité

```R
# Tracé du diamètre du réseau
ggplot(network_evolution_month, aes(x = Date, y = Diameter)) +
    geom_line(color = "purple") +
    labs(title = "Évolution du diamètre du réseau par mois", x = "Date", y = "Diamètre") +
    theme_minimal()

# Tracé de l'assortativité par degré
ggplot(network_evolution_month, aes(x = Date, y = Assortativity)) +
    geom_line(color = "red") +
    labs(title = "Évolution de l'assortativité par mois", x = "Date", y = "Assortativité") +
    theme_minimal()
```

Évolution de la Modularité et du Nombre de Communautés

```R
# Tracé de la modularité
ggplot(network_evolution_month, aes(x = Date, y = Modularity)) +
    geom_line(color = "orange") +
    labs(title = "Évolution de la modularité par mois", x = "Date", y = "Modularité") +
    theme_minimal()

# Tracé du nombre de communautés
ggplot(network_evolution_month, aes(x = Date, y = Num_Communities)) +
    geom_line(color = "brown") +
    labs(title = "Évolution du nombre de communautés par mois", x = "Date", y = "Nombre de communautés") +
    theme_minimal()
```

---

#### 2.5. Analyse de l'Évolution des Communautés

Pour étudier l'évolution des communautés, nous pouvons comparer les partitions de communautés entre les périodes.

**Comparaison des Communautés entre Périodes Consécutives**

Nous utiliserons l'**indice de Rand ajusté (ARI)** pour mesurer la similarité entre les partitions de communautés.

Installation du Package `aricode`

```R
if (!requireNamespace("aricode", quietly = TRUE)) {
    install.packages("aricode")
}
library(aricode)
```

Calcul de l'ARI entre Périodes

```R
# Initialiser un dataframe pour stocker les ARI
community_similarity <- data.frame(
    Period1 = character(),
    Period2 = character(),
    ARI = numeric(),
    stringsAsFactors = FALSE
)

# Liste des périodes ordonnées
periods <- sort(names(graphs_by_month))

# Parcourir les périodes consécutives
for (i in 2:length(periods)) {
    prev_period <- periods[i - 1]
    current_period <- periods[i]
    
    g_prev <- graphs_by_month[[prev_period]]
    g_curr <- graphs_by_month[[current_period]]
    
    # Vérifier si les graphes ont des nœuds et des liens
    if (vcount(g_prev) > 0 && ecount(g_prev) > 0 && vcount(g_curr) > 0 && ecount(g_curr) > 0) {
        # Détection des communautés
        communities_prev <- cluster_louvain(g_prev)
        communities_curr <- cluster_louvain(g_curr)
        
        # Obtenir les memberships
        membership_prev <- membership(communities_prev)
        membership_curr <- membership(communities_curr)
        
        # Obtenir les nœuds communs entre les deux périodes
        common_nodes <- intersect(names(membership_prev), names(membership_curr))
        
        # Filtrer les memberships pour les nœuds communs
        mem_prev_filtered <- membership_prev[common_nodes]
        mem_curr_filtered <- membership_curr[common_nodes]
        
        # Calculer l'ARI
        ari_value <- ARI(mem_prev_filtered, mem_curr_filtered)
    } else {
        ari_value <- NA
    }
    
    # Ajouter le résultat au dataframe
    community_similarity <- rbind(community_similarity, data.frame(
        Period1 = prev_period,
        Period2 = current_period,
        ARI = ari_value,
        stringsAsFactors = FALSE
    ))
}
```

Visualisation de l'Évolution de la Similarité des Communautés

```R
# Convertir les périodes en format date
community_similarity$Date <- as.Date(paste0(community_similarity$Period2, "-01"))

# Tracé de l'ARI au fil du temps
ggplot(community_similarity, aes(x = Date, y = ARI)) +
    geom_line(color = "magenta") +
    labs(title = "Évolution de la similarité des communautés (ARI)", x = "Date", y = "Indice de Rand ajusté (ARI)") +
    theme_minimal()
```

**Interprétation :**

- Un **ARI élevé** indique une forte similarité des communautés entre les périodes.
- Un **ARI faible** suggère des changements significatifs dans la structure des communautés.

---

#### 2.6. Analyse Globale

En combinant ces métriques, vous pouvez :

- **Identifier les tendances** : Croissance du réseau, changements structurels, évolution des communautés.
- **Détecter les événements clés** : Pics ou chutes soudaines dans les métriques peuvent indiquer des événements importants.
- **Comprendre les dynamiques** : Comment les interactions évoluent, comment les communautés se forment ou se dissolvent.
Conseils pour l'Interprétation

- **Contexte** : Reliez les changements observés à des événements ou des phénomènes externes.
- **Comparaison des métriques** : Cherchez des corrélations entre les métriques pour approfondir l'analyse.
- **Visualisation** : Utilisez des graphiques pour faciliter la compréhension des tendances.
### 3. Étude des Tendances Relationnelles Globales

Après avoir calculé diverses métriques pour chaque période temporelle (par mois ou par année), nous pouvons étudier les **tendances relationnelles globales** du réseau au fil du temps. Cela nous permettra d'identifier des phénomènes tels que la **croissance du réseau**, la **densification**, la **formation de hubs**, les **changements dans l'assortativité**, et l'**évolution des modèles de clustering**.

- **Identifier les tendances globales** dans l'évolution du réseau.
- **Analyser la distribution des degrés** et son évolution au fil du temps.
- **Tester l'hypothèse d'attachement préférentiel** pour comprendre les mécanismes de croissance du réseau.
- **Interpréter les résultats** pour mieux comprendre la dynamique du réseau.

#### 3.1. Test de l'Attachement Préférentiel

**Hypothèse d'Attachement Préférentiel**

L'attachement préférentiel suggère que les nouveaux nœuds ont tendance à se connecter aux nœuds déjà bien connectés, ce qui conduit à la formation de hubs.

**Analyse de la Corrélation entre l'Âge des Nœuds et leur Degré**

Attribution de l'Âge aux Nœuds : Nous allons estimer l'âge des nœuds en fonction de leur première apparition dans les données.

```R
# Obtenir la liste des périodes 
periods <- names(graphs_by_month)

# Initialiser un dataframe pour stocker l'âge des nœuds
node_ages <- data.frame(
    node = character(),
    birth_period = character(),
    age = integer(),
    stringsAsFactors = FALSE
)

# Parcourir les périodes pour déterminer l'âge des nœuds
for (i in seq_along(periods)) {
    period <- periods[i]
    g <- graphs_by_month[[period]]
    nodes_in_period <- V(g)$name
    
    # Ajouter les nœuds qui apparaissent pour la première fois
    new_nodes <- setdiff(nodes_in_period, node_ages$node)
    if (length(new_nodes) > 0) {
        node_ages <- rbind(node_ages, data.frame(
            node = new_nodes,
            birth_period = period,
            age = i,  # L'âge est défini par l'indice de la période
            stringsAsFactors = FALSE
        ))
    }
}

# Mettre à jour l'âge des nœuds pour la dernière période
g_last <- graphs_by_month[[tail(periods, n=1)]]
degrees_last <- degree(g_last)
age_degree_data <- merge(node_ages, data.frame(node = names(degrees_last), degree = degrees_last), by = "node")
```

Visualisation de la Relation entre l'Âge et le Degré

```R
# Convertir l'âge en numérique (période actuelle moins période de naissance)
age_degree_data$age_in_periods <- length(periods) - match(age_degree_data$birth_period, periods) + 1

# Tracé de la relation âge-degré
ggplot(age_degree_data, aes(x = age_in_periods, y = degree)) +
    geom_point(alpha = 0.5) +
    geom_smooth(method = "lm", color = "red") +
    labs(title = "Relation entre l'âge des nœuds et leur degré à la dernière période", x = "Âge du nœud (en périodes)", y = "Degré") +
    theme_minimal()
```

**Interprétation :**

- **Corrélation Positive** : Une tendance ascendante suggère que les nœuds plus anciens ont accumulé plus de liens, ce qui est cohérent avec l'attachement préférentiel.
- **Absence de Corrélation** : Indique que l'âge n'est pas un facteur déterminant dans l'acquisition de liens, suggérant d'autres mécanismes à l'œuvre.

**Calcul du Coefficient de Corrélation**

Nous pouvons quantifier la relation entre l'âge et le degré en calculant le coefficient de corrélation de Pearson.

```R
# Calcul du coefficient de corrélation
correlation <- cor(age_degree_data$age_in_periods, age_degree_data$degree, method = "pearson")
cat("Le coefficient de corrélation entre l'âge et le degré est :", correlation, "\n")
```

**Interprétation :**

- **Coefficient proche de 1** : Forte corrélation positive.
- **Coefficient proche de 0** : Pas de corrélation.
- **Coefficient négatif** : Corrélation négative (rare dans ce contexte).

#### 3.2. Analyse de la Formation de Hubs

Dans cette section, nous souhaitons :

- **Identifier les nœuds hubs** : Ceux dont le degré est significativement plus élevé que la moyenne.
- **Analyser l'évolution du degré des hubs au fil du temps** : Pour voir s'ils continuent à accumuler des liens ou s'ils perdent de leur influence.

Pour ce faire, nous utiliserons :

- **Les graphes découpés par période** générés par la fonction `graphcut`.
- **Les données d'âge et de degré des nœuds** calculées précédemment.

#### Préparation des Données

Avant d'exécuter le code de cette section, nous devons nous assurer que les variables suivantes sont correctement définies :

- `age_degree_data` : Contient les informations sur l'âge des nœuds et leur degré à la dernière période.
- `graphs_by_month` ou `graphs_by_period` : Une liste de graphes découpés par période.
- `periods` : Un vecteur contenant les noms des périodes, correspondant aux noms des graphes dans `graphs_by_month`.

**Assurons-nous que ces variables sont correctement définies à partir de la fonction `graphcut` :**

```R
# Supposons que nous avons déjà chargé les données 'links' et défini la fonction 'graphcut'

# Générer les graphes par mois
graphs_by_month <- graphcut(links, step = "month")

# Obtenir la liste des périodes
periods <- names(graphs_by_month)
```

#### Calcul de `age_degree_data`

Nous avons déjà calculé `age_degree_data` dans la section précédente, en attribuant un âge aux nœuds et en calculant leur degré à la dernière période.

```R
# Initialiser un dataframe pour stocker l'âge des nœuds
node_ages <- data.frame(
    node = character(),
    birth_period = character(),
    age = integer(),
    stringsAsFactors = FALSE
)

# Parcourir les périodes pour déterminer l'âge des nœuds
for (i in seq_along(periods)) {
    period <- periods[i]
    g <- graphs_by_month[[period]]
    nodes_in_period <- V(g)$name

    # Ajouter les nœuds qui apparaissent pour la première fois
    new_nodes <- setdiff(nodes_in_period, node_ages$node)
    if (length(new_nodes) > 0) {
        node_ages <- rbind(node_ages, data.frame(
            node = new_nodes,
            birth_period = period,
            age = i,
            stringsAsFactors = FALSE
        ))
    }
}

# Graphe de la dernière période
g_last <- graphs_by_month[[tail(periods, n=1)]]
degrees_last <- degree(g_last)

# Fusionner les informations d'âge et de degré
age_degree_data <- merge(node_ages, data.frame(node = names(degrees_last), degree = degrees_last), by = "node")
```

#### Identification des Nœuds Hubs

**Code à vérifier :**

```R
# Calcul du degré moyen et de l'écart-type
mean_degree <- mean(age_degree_data$degree)
sd_degree <- sd(age_degree_data$degree)

# Seuil pour définir un hub (par exemple, degré supérieur à moyenne + 2 écart-types)
threshold <- mean_degree + 2 * sd_degree

# Identification des hubs
hubs <- age_degree_data[age_degree_data$degree > threshold, ]

# Affichage des hubs
print(hubs)
```

**Vérification :**

- **Variables utilisées :**
  - `age_degree_data$degree` : Le degré des nœuds à la dernière période.
- **Calcul du seuil pour définir un hub :**
  - Un nœud est considéré comme un hub si son degré est supérieur à `mean_degree + 2 * sd_degree`.
- **Extraction des hubs :**
  - Nous filtrons `age_degree_data` pour obtenir les nœuds dont le degré dépasse ce seuil.

**Conclusion :**

- Le code est cohérent avec les données issues de la fonction `graphcut`.
- Les variables utilisées sont correctement définies.
- Aucune modification n'est nécessaire pour cette partie.


### Évolution du Degré des Hubs au Fil du Temps

**Code à vérifier :**

```R
# Sélection des nœuds hubs
hub_nodes <- hubs$node

# Initialiser un dataframe pour stocker l'évolution des degrés
hub_degree_evolution <- data.frame(
    Period = character(),
    Node = character(),
    Degree = integer(),
    stringsAsFactors = FALSE
)

# Parcourir les périodes et enregistrer le degré des hubs
for (period in periods) {
    g <- graphs_by_month[[period]]
    degrees <- degree(g)
    for (node in hub_nodes) {
        if (node %in% names(degrees)) {
            degree_value <- degrees[node]
        } else {
            degree_value <- 0
        }
        hub_degree_evolution <- rbind(hub_degree_evolution, data.frame(
            Period = period,
            Node = node,
            Degree = degree_value,
            stringsAsFactors = FALSE
        ))
    }
}

# Visualisation de l'évolution du degré des hubs
ggplot(hub_degree_evolution, aes(x = as.Date(paste0(Period, "-01")), y = Degree, color = Node, group = Node)) +
    geom_line() +
    geom_point() +
    labs(title = "Évolution du degré des hubs au fil du temps", x = "Date", y = "Degré") +
    theme_minimal()
```

**Vérification :**

- **Variables utilisées :**
  - `hub_nodes` : Les noms des nœuds hubs identifiés précédemment.
  - `periods` : Les noms des périodes (par exemple, "2022-01", "2022-02", ...).
  - `graphs_by_month` : La liste des graphes par mois générés par `graphcut`.
- **Boucle sur les périodes :**
  - Pour chaque période, on extrait le graphe correspondant et calcule les degrés des nœuds.
  - On enregistre le degré de chaque hub pour chaque période.
- **Construction du dataframe `hub_degree_evolution` :**
  - Contient les colonnes `Period`, `Node`, `Degree`.
- **Visualisation :**
  - Utilise `ggplot2` pour tracer l'évolution du degré des hubs au fil du temps.
  - `aes(x = as.Date(paste0(Period, "-01")), y = Degree, color = Node, group = Node)` :
    - `x` : La date correspondant à la période (on ajoute "-01" pour avoir une date valide).
    - `y` : Le degré du nœud.
    - `color` et `group` : Par nœud, pour tracer une ligne par hub.

### Interprétation

Après avoir exécuté ce code :

- **Si le degré des hubs augmente au fil du temps :**
  - Cela suggère que les hubs continuent d'attirer de nouveaux liens.
  - Confirme le phénomène d'attachement préférentiel.
- **Si le degré des hubs stagne ou diminue :**
  - Les hubs perdent de leur influence.
  - Le réseau pourrait évoluer vers une structure différente.

## Références

- **Barabási, A.-L., & Albert, R. (1999).** "Emergence of Scaling in Random Networks". *Science*, 286(5439), 509-512.
- **Newman, M. E. J. (2003).** "The Structure and Function of Complex Networks". *SIAM Review*, 45(2), 167-256.
- **Price, D. J. de S. (1965).** "Networks of Scientific Papers". *Science*, 149(3683), 510-515.
- **Watts, D. J., & Strogatz, S. H. (1998).** "Collective Dynamics of 'Small-World' Networks". *Nature*, 393(6684), 440-442.