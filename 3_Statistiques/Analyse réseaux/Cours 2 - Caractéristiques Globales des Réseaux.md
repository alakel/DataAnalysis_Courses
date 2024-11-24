Dans ce cours, nous allons explorer les caractéristiques globales des réseaux sociaux, en mettant l'accent sur les mesures fondamentales qui permettent de décrire et d'analyser la structure d'un réseau. Comprendre ces caractéristiques est essentiel pour appréhender la dynamique des interactions au sein des réseaux et pour identifier les patterns qui influencent la diffusion de l'information, la formation de communautés, et la robustesse des réseaux face aux perturbations.

### Objectifs du cours

- **Comprendre les mesures de base utilisées pour décrire les réseaux sociaux.**
- **Apprendre à calculer la taille d'un réseau, la distribution des degrés, le degré moyen et l'écart-type des degrés.**
- **Découvrir les réseaux à invariant d'échelle et leur importance dans la compréhension des réseaux réels.**
- **Acquérir des compétences pratiques en utilisant le langage R pour analyser des réseaux à partir de données.**

---

### 1. Taille du Réseau : Nombre de Nœuds et de Liens

#### 1.1. Définition

La **taille d'un réseau** est l'une des mesures les plus fondamentales en analyse de réseau. Elle se caractérise par :

- **Nombre de nœuds (ou sommets)** : Il s'agit du nombre total d'entités individuelles dans le réseau. Dans un réseau social, les nœuds peuvent représenter des personnes, des organisations, des sites web, etc.
- **Nombre de liens (ou arêtes)** : C'est le nombre total de connexions entre les nœuds. Un lien peut représenter une relation d'amitié, une interaction, une citation, etc.

#### 1.2. Importance

- **Compréhension de l'échelle** : Savoir combien de nœuds et de liens contient un réseau donne une idée de son ampleur et de sa complexité.
- **Calcul d'autres mesures** : De nombreuses autres métriques dépendent du nombre de nœuds et de liens, comme la densité du réseau.
- **Comparaison entre réseaux** : La taille permet de comparer différents réseaux entre eux.

#### 1.3. Exemple avec R

Supposons que nous ayons deux fichiers :

- `noeud.txt` : Contient la liste des nœuds du réseau.
- `links.txt` : Contient la liste des liens entre les nœuds.

**Format des fichiers**

**noeud.txt** (format CSV) :

```
id,label
1,Alice
2,Bob
3,Charlie
...
```

**links.txt** (format CSV) :

```
source,target
1,2
2,3
1,3
...
```

**Chargement des données et calcul de la taille du réseau**

```R
# Installation des packages nécessaires
install.packages("igraph")
library(igraph)

# Chargement des nœuds
nodes <- read.csv("noeud.txt", header = TRUE, stringsAsFactors = FALSE)

# Chargement des liens
links <- read.csv("links.txt", header = TRUE, stringsAsFactors = FALSE)

# Création du graphe
g <- graph_from_data_frame(d = links, vertices = nodes, directed = FALSE)

# Calcul du nombre de nœuds et de liens
num_nodes <- vcount(g)
num_links <- ecount(g)

# Affichage des résultats
cat("Le réseau contient", num_nodes, "nœuds et", num_links, "liens.\n")
```

**Explication du code :**

- **igraph** : Un package R puissant pour l'analyse et la manipulation des réseaux.
- **graph_from_data_frame** : Fonction pour créer un graphe à partir de data frames contenant les liens et les nœuds.
- **vcount(g)** : Renvoie le nombre de nœuds dans le graphe `g`.
- **ecount(g)** : Renvoie le nombre de liens dans le graphe `g`.

---

### 2. Distribution des Degrés et Réseaux à Invariant d'Échelle

#### 2.1. Définition du Degré

- **Degré d'un nœud** : Le nombre de liens connectés à ce nœud.
  - **Degré entrant (indegree)** : Pour les graphes orientés, le nombre de liens qui pointent vers le nœud.
  - **Degré sortant (outdegree)** : Le nombre de liens qui partent du nœud.

#### 2.2. Distribution des Degrés

- La **distribution des degrés** décrit comment les degrés des nœuds sont répartis dans le réseau.
- Elle est souvent représentée par une fonction qui donne la probabilité qu'un nœud ait un certain degré.

#### 2.3. Réseaux à Invariant d'Échelle (Scale-Free Networks)

- **Concept** : Introduit par Barabási et Albert en 1999, un réseau à invariant d'échelle est un réseau dont la distribution des degrés suit une loi de puissance.
- **Caractéristiques** :
  - **Présence de hubs** : Quelques nœuds ont un degré très élevé, tandis que la majorité des nœuds ont un faible degré.
  - **Robustesse et vulnérabilité** :
    - **Robuste** face à la suppression aléatoire de nœuds.
    - **Vulnérable** aux attaques ciblant les hubs.
- **Importance** :
  - De nombreux réseaux réels (Internet, réseaux sociaux, réseaux métaboliques) présentent une distribution des degrés suivant une loi de puissance.

#### 2.4. Calcul et Visualisation de la Distribution des Degrés

**Code R pour calculer et visualiser la distribution des degrés**

```R
# Calcul du degré de chaque nœud
degrees <- degree(g, mode = "all")

# Affichage des degrés
head(degrees)

# Distribution des degrés
deg_dist <- degree_distribution(g, cumulative = FALSE, mode = "all")

# Tracé de la distribution des degrés
plot(x = 0:(length(deg_dist)-1), y = deg_dist, type = "h", main = "Distribution des degrés", xlab = "Degré", ylab = "Fréquence")

# Tracé en échelle log-log pour détecter une loi de puissance
plot(degree_distribution(g, cumulative = TRUE, mode = "all"), log = "xy", main = "Distribution cumulative des degrés (log-log)", xlab = "Degré", ylab = "P(k)")
```

**Explication du code :**

- **degree** : Calcule le degré de chaque nœud.
- **degree_distribution** : Calcule la distribution des degrés.
  - **cumulative = TRUE** : Utilisé pour la distribution cumulative, utile pour les tracés en log-log.
- **plot** : Fonction de base pour tracer les graphiques.
- **log = "xy"** : Applique l'échelle logarithmique aux axes x et y.

#### Interprétation

- Si la distribution des degrés suit une ligne droite sur le graphique log-log, cela suggère une loi de puissance, caractéristique des réseaux à invariant d'échelle.
- **Observation des hubs** : En analysant les degrés élevés, on peut identifier les nœuds qui jouent un rôle central dans le réseau.

---

### 3. Degré Moyen et Écart-Type des Degrés

#### 3.1. Degré Moyen

- **Définition** : Le degré moyen est la moyenne des degrés de tous les nœuds du réseau.
- **Calcul** :

$$
  k_{\text{moyen}} = \frac{2 \times \text{nombre de liens}}{\text{nombre de nœuds}}
$$

- **Importance** :
  - Donne une idée générale de la connectivité du réseau.
  - Utile pour comparer des réseaux de tailles différentes.

#### 3.2. Écart-Type des Degrés

- **Définition** : L'écart-type des degrés mesure la dispersion des degrés autour de la moyenne.
- **Calcul** : Utilise la formule standard de l'écart-type pour les données.

#### 3.3. Code R pour calculer le degré moyen et l'écart-type

```R
# Degré moyen
mean_degree <- mean(degrees)
cat("Le degré moyen du réseau est :", mean_degree, "\n")

# Écart-type des degrés
sd_degree <- sd(degrees)
cat("L'écart-type des degrés est :", sd_degree, "\n")
```

**Explication du code :**

- **mean(degrees)** : Calcule la moyenne des degrés.
- **sd(degrees)** : Calcule l'écart-type des degrés.

#### 3.4. Interprétation

- **Degré moyen élevé** : Indique que les nœuds ont, en moyenne, de nombreuses connexions. Le réseau est donc dense.
- **Écart-type élevé** : Signifie qu'il y a une grande variation dans les degrés des nœuds. Certains nœuds peuvent être des hubs, tandis que d'autres sont peu connectés.
- **Analyse conjointe** : En combinant le degré moyen et l'écart-type, on obtient une image plus complète de la structure du réseau.
# Annexe : la fonction AnalyseNet

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
### Conclusion du Cours

Dans ce cours, nous avons exploré les caractéristiques globales des réseaux, en nous concentrant sur :

- **La taille du réseau** : Comprendre le nombre de nœuds et de liens nous donne une première idée de la complexité du réseau.
- **La distribution des degrés** : Cette mesure nous informe sur la connectivité des nœuds et la présence éventuelle de hubs.
- **Les réseaux à invariant d'échelle** : De nombreux réseaux réels suivent une distribution des degrés selon une loi de puissance, ce qui a des implications importantes pour leur structure et leur dynamique.
- **Le degré moyen et l'écart-type** : Ces statistiques descriptives nous aident à comprendre la connectivité générale du réseau et la variation entre les nœuds.

Nous avons également mis en pratique ces concepts en utilisant R pour analyser un réseau fictif. Les activités proposées vous permettent d'appliquer ces notions et d'explorer les outils de visualisation disponibles.

**Points clés à retenir :**

- Les mesures globales sont essentielles pour comprendre la structure et le comportement d'un réseau.
- Les hubs jouent un rôle crucial dans la connectivité et la robustesse des réseaux.
- Les outils comme R, Gephi, et NetworkX sont précieux pour l'analyse et la visualisation des réseaux.

**Prochain cours :** Nous approfondirons les mesures de distance dans les réseaux et explorerons la théorie du "petit monde", ainsi que ses implications pour la diffusion de l'information.

### Bibliographie pour aller plus loin

1. **Barabási, A.-L., & Albert, R. (1999).** Emergence of scaling in random networks. *Science*, 286(5439), 509–512.  
   Cet article fondateur introduit le modèle d'attachement préférentiel et explique l'émergence de réseaux sans échelle, où quelques nœuds hautement connectés jouent un rôle central.

2. **Newman, M. E. J. (2003).** The structure and function of complex networks. *SIAM Review*, 45(2), 167–256.  
   Une revue exhaustive des propriétés structurelles des réseaux complexes, couvrant des sujets tels que la distribution des degrés, le clustering, la centralité et les communautés.

3. **Watts, D. J., & Strogatz, S. H. (1998).** Collective dynamics of 'small-world' networks. *Nature*, 393(6684), 440–442.  
   Cet article présente le modèle des réseaux petits mondes, démontrant que de nombreux réseaux réels combinent une forte clustering locale avec de courtes distances globales entre les nœuds.

4. **Albert, R., & Barabási, A.-L. (2002).** Statistical mechanics of complex networks. *Reviews of Modern Physics*, 74(1), 47–97.  
   Un examen approfondi des avancées dans la compréhension des réseaux complexes, abordant les propriétés statistiques, les modèles de génération de réseaux et les phénomènes dynamiques.

5. **Newman, M. (2010).** *Networks: An Introduction*. Oxford University Press.  
   Un ouvrage de référence offrant une introduction complète aux réseaux, incluant les mesures globales, les modèles de réseaux et les méthodes d'analyse.