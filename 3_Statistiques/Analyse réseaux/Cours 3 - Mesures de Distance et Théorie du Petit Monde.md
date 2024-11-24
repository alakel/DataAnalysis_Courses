
### 1. Distances Géodésiques et Diamètre du Réseau

#### 1.1. Distances Géodésiques

**Définition**

- **Distance géodésique** : La distance géodésique entre deux nœuds est la longueur du plus court chemin les reliant dans le réseau.
  - **Chemin** : Séquence de nœuds où chaque nœud est connecté au suivant par une arête.
  - **Longueur du chemin** : Nombre d'arêtes traversées pour aller d'un nœud à un autre.

**Importance**

- **Mesure de proximité** : La distance géodésique indique à quel point deux nœuds sont proches l'un de l'autre dans le réseau.
- **Influence sur la diffusion** : Plus la distance entre deux nœuds est courte, plus il est probable qu'une information ou une influence passe rapidement de l'un à l'autre.
- **Analyse de la cohésion** : Des distances géodésiques globalement courtes suggèrent un réseau bien connecté.

**Calcul en R**

**Calcul des distances géodésiques**

```R
# Matrice des distances géodésiques entre tous les nœuds
dist_matrix <- distances(g)

# Affichage de la matrice des distances pour les premiers nœuds
print(dist_matrix[1:5, 1:5])
```

**Explication du code :**

- **distances(g)** : Calcule la matrice des distances géodésiques entre tous les couples de nœuds du graphe `g`.
- La matrice résultante a pour dimensions le nombre de nœuds du réseau.

**Interprétation**

- Les entrées de la matrice représentent la distance minimale entre deux nœuds.
- Une valeur élevée indique que deux nœuds sont éloignés dans le réseau.
- Une valeur infinie (Inf) signifie qu'il n'y a pas de chemin entre les deux nœuds (le réseau n'est pas connexe).

#### 1.2. Diamètre du Réseau

**Définition**

- **Diamètre du réseau** : C'est la plus grande distance géodésique minimale entre toutes les paires de nœuds du réseau.
  - Formule : 
$$
\text{Diamètre} = \max_{i,j} d(i,j)
$$
  - Où \( d(i,j) \) est la distance géodésique entre les nœuds \( i \) et \( j \).

**Importance**

- **Indicateur de la taille du réseau** en termes de distance.
- **Impact sur la diffusion** : Un diamètre faible suggère que l'information peut potentiellement se propager rapidement à travers le réseau.

**Calcul en R**

```R
# Calcul du diamètre du réseau
network_diameter <- diameter(g, directed = FALSE, unconnected = TRUE)
cat("Le diamètre du réseau est :", network_diameter, "\n")
```

**Explication du code :**

- **diameter(g, directed = FALSE, unconnected = TRUE)** : Calcule le diamètre du graphe `g`.
  - **directed = FALSE** : Indique que le graphe est non orienté.
  - **unconnected = TRUE** : Si le graphe n'est pas connexe, considère les distances infinies.

**Interprétation**

- **Diamètre faible** : Le réseau est "petit" en termes de distance ; les nœuds sont proches les uns des autres.
- **Diamètre élevé** : Les nœuds les plus éloignés sont très distants, ce qui peut ralentir la propagation.

#### 1.3. Distance Moyenne

**Définition**

- **Distance géodésique moyenne** : Moyenne des distances géodésiques minimales entre toutes les paires de nœuds connectés du réseau.
  - Formule : 
$$
  \bar{d} = \frac{1}{N(N-1)} \sum_{i \neq j} d(i,j)
$$
  - Où \( N \) est le nombre de nœuds.

**Importance**

- **Mesure globale de la proximité** : Indique, en moyenne, à quelle distance se trouvent les nœuds du réseau.
- **Comparaison entre réseaux** : Permet de comparer la cohésion de différents réseaux.

**Calcul en R**

```R
# Calcul de la distance géodésique moyenne
average_path_length <- mean_distance(g, directed = FALSE)
cat("La distance géodésique moyenne du réseau est :", average_path_length, "\n")
```

**Explication du code :**

- **mean_distance(g, directed = FALSE)** : Calcule la distance moyenne des chemins les plus courts dans le graphe `g`.
### 2. Transitivité et Coefficient de Clustering

Avant d'aborder la théorie du "petit monde", il est essentiel de comprendre les concepts de **transitivité** et de **coefficient de clustering** dans les réseaux sociaux. Ces mesures nous permettent d'évaluer la tendance des nœuds à former des triangles ou des groupes fortement connectés, ce qui a des implications importantes pour la cohésion du réseau et la propagation de l'information.
#### 2.1. Définition

- **Transitivité** : En théorie des graphes, la transitivité mesure la probabilité que deux nœuds connectés à un même nœud soient également connectés entre eux.
- En d'autres termes, si le nœud **A** est connecté à **B**, et **B** est connecté à **C**, la transitivité examine la probabilité que **A** soit également connecté à **C**.

#### 2.2. Importance

- **Formation de Triades** : La transitivité est liée à la formation de triangles dans le réseau.
- **Cohésion Sociale** : Une transitivité élevée suggère une tendance à former des groupes fermés où tout le monde connaît tout le monde.
- **Propagation de l'Information** : Affecte la redondance des chemins pour la diffusion de l'information.

#### 2.3. Mesure de la Transitivité Globale

- **Transitivité Globale (Coefficient de Clustering Global)** : Elle est calculée en prenant le rapport entre le nombre de triangles fermés et le nombre de triplets connectés dans le réseau.
$$
  C = \frac{3 \times \text{Nombre de triangles fermés}}{\text{Nombre de triplets connectés}}
$$  
  - **Triplet connecté** : Un ensemble de trois nœuds où au moins deux liens existent.
  - **Triangle fermé** : Un triplet où chaque nœud est connecté aux deux autres (triangle complet).

#### 2.4. Calcul en R

**Calcul de la transitivité globale**

```R
# Calcul de la transitivité globale
transitivity_global <- transitivity(g, type = "global")
cat("La transitivité globale du réseau est :", transitivity_global, "\n")
```

**Explication du code :**

- **transitivity(g, type = "global")** : Calcule le coefficient de clustering global du graphe `g`.
- **type = "global"** : Indique que nous calculons la transitivité globale.

**Interprétation**

- **Valeur proche de 1** : Indique une transitivité élevée ; le réseau a tendance à former de nombreux triangles.
- **Valeur proche de 0** : Indique une transitivité faible ; peu de triangles sont présents.

---

### 3. Coefficient de Clustering d'un noeud

#### 3.1. Coefficient de Clustering Local

- **Définition** : Pour un nœud donné, le coefficient de clustering local mesure la proportion de paires de voisins de ce nœud qui sont connectés entre eux.
  

$$
  C_i = \frac{2 \times \text{Nombre de liens entre les voisins de } i}{k_i (k_i - 1)}
$$
  
  - Où \( k_i \) est le degré du nœud \( i \).
  - Le **numérateur** compte le nombre de liens existants entre les voisins du nœud \( i \).
  - Le dénominateur représente le nombre maximal possible de liens entre ces voisins.

#### 3.2. Importance

- **Analyse Fine** : Le coefficient de clustering local permet d'identifier les nœuds qui sont au centre de communautés fortement connectées.
- **Détection de Communautés** : Les nœuds avec un coefficient de clustering élevé sont souvent au sein de clusters ou de communautés.

#### 3.3. Calcul en R

**Calcul du coefficient de clustering local pour chaque nœud**

```R
# Calcul du coefficient de clustering local pour chaque nœud
clustering_local <- transitivity(g, type = "local")

# Affichage des coefficients pour les premiers nœuds
head(clustering_local)
```

**Explication du code :**

- **transitivity(g, type = "local")** : Calcule le coefficient de clustering local pour chaque nœud du graphe `g`.

**Calcul du coefficient de clustering moyen du réseau**

```R
# Calcul du coefficient de clustering moyen
clustering_mean <- mean(clustering_local, na.rm = TRUE)
cat("Le coefficient de clustering moyen est :", clustering_mean, "\n")
```

**Note :** Certaines valeurs peuvent être `NaN` (par exemple, pour les nœuds de degré 0 ou 1). L'argument `na.rm = TRUE` permet d'ignorer ces valeurs lors du calcul de la moyenne.

#### 3.4. Interprétation

- **Coefficient élevé (>0.5)** : Indique que les voisins du nœud sont fortement connectés entre eux.
- **Coefficient faible (~0)** : Les voisins du nœud sont peu ou pas connectés entre eux.
- **Analyse du clustering moyen** : Donne une idée de la tendance générale du réseau à former des clusters.

---

### 4. Relation entre Transitivité et Clustering

- **Similarités** : La transitivité globale et le coefficient de clustering global sont souvent utilisés de manière interchangeable.
- **Différences Subtiles** :
  - La **transitivité globale** considère les triangles fermés par rapport à tous les triplets connectés.
  - Le **coefficient de clustering** peut être calculé de manière locale (par nœud) ou globale (moyenne des coefficients locaux).

#### 4.1. Comparaison des Mesures en R

```R
# Calcul de la transitivité globale
transitivity_global <- transitivity(g, type = "global")

# Calcul du coefficient de clustering moyen
clustering_mean <- transitivity(g, type = "average")

# Affichage des résultats
cat("Transitivité globale :", transitivity_global, "\n")
cat("Coefficient de clustering moyen :", clustering_mean, "\n")
```

**Explication du code :**

- **transitivity(g, type = "average")** : Calcule le coefficient de clustering moyen (moyenne des coefficients locaux).

#### 4.2. Interprétation

- **Transitivité globale vs. Clustering moyen** :
  - Les deux mesures peuvent différer en valeur.
  - La transitivité globale est influencée par les nœuds de haut degré.
  - Le clustering moyen donne un poids égal à chaque nœud, quelle que soit sa connectivité.

---

### 5. Implications pour la Formation de Communautés et le "Communautarisme"

#### 5.1. Formation de Communautés

- **Communautés** : Groupes de nœuds avec des connexions internes denses et moins de connexions avec le reste du réseau.
- **Clustering Élevé** : Indique une tendance naturelle à former des communautés.
- **Rôle des Triangles** : Les triangles sont les unités de base des communautés, facilitant la cohésion interne.

#### 5.2. "Communautarisme" dans les Réseaux Sociaux

- **Définition** : Tendance des individus à se regrouper avec des personnes similaires ou avec lesquelles ils ont des liens forts.
- **Homophilie** : Préférence pour les interactions avec des pairs partageant des caractéristiques communes.
- **Effet sur le Réseau** :
  - Renforce les liens internes.
  - Peut conduire à des bulles sociales ou des silos d'information.
  - Influence la diffusion de l'information et la polarisation des opinions.

#### 5.3. Mesurer la Tendance au "Communautarisme"

- **Coefficient de Clustering Élevé** : Suggère une forte cohésion interne et une possible homogénéité au sein des groupes.
- **Analyse des Communautés** :
  - Détection des communautés à l'aide d'algorithmes spécifiques (par exemple, Louvain, Infomap).
  - Étude des attributs des nœuds pour vérifier l'homogénéité au sein des communautés.

---

#### 5.4. Exemple Pratique en R

**Visualisation du Réseau avec les Clustering Locaux**

```R
# Chargement du package supplémentaire pour la visualisation
# install.packages("RColorBrewer")
library(RColorBrewer)

# Attribution des coefficients de clustering locaux aux nœuds
V(g)$clustering <- clustering_local

# Définition d'une palette de couleurs
palette <- colorRampPalette(brewer.pal(9, "YlOrRd"))(100)

# Normalisation des valeurs pour correspondre à la palette
clustering_norm <- (V(g)$clustering - min(V(g)$clustering, na.rm = TRUE)) / (max(V(g)$clustering, na.rm = TRUE) - min(V(g)$clustering, na.rm = TRUE))
colors <- palette[as.numeric(cut(clustering_norm, breaks = 100))]

# Visualisation du réseau
plot(g, vertex.color = colors, vertex.label = NA, main = "Réseau avec coefficients de clustering locaux")
```

**Explication du code :**

- **V(g)$clustering** : Stocke le coefficient de clustering local dans les attributs des nœuds.
- **colorRampPalette** et **brewer.pal** : Utilisés pour créer une palette de couleurs.
- **Normalisation des valeurs** : Permet d'assigner une couleur à chaque nœud en fonction de son coefficient de clustering.
- **plot** : Fonction de visualisation du réseau, où la couleur des nœuds reflète leur clustering local.

**Analyse**

- **Observation Visuelle** : Les nœuds avec des couleurs plus chaudes (rouge/orange) ont un coefficient de clustering plus élevé.
- **Identification des Communautés** : Les zones du réseau où les nœuds sont majoritairement de couleur chaude peuvent correspondre à des communautés fortement connectées.

#### Conclusion du 5

Dans ce chapitre, nous avons exploré les concepts de **transitivité** et de **coefficient de clustering** dans les réseaux sociaux, qui sont essentiels pour comprendre la tendance des nœuds à former des groupes fortement connectés. Ces mesures permettent d'évaluer la cohésion interne du réseau et d'identifier les communautés potentielles.

**Points clés à retenir :**

- La **transitivité** mesure la probabilité que les nœuds connectés à un même nœud soient également connectés entre eux.
- Le **coefficient de clustering local** indique à quel point les voisins d'un nœud sont connectés entre eux.
- Un **clustering élevé** est souvent associé à la formation de communautés et peut influencer la diffusion de l'information.
- Comprendre ces mesures est crucial avant d'aborder la **théorie du petit monde**, qui combine un **clustering élevé** avec une **distance géodésique moyenne faible**.

En maîtrisant ces concepts, vous serez mieux équipés pour analyser la structure des réseaux sociaux et comprendre les dynamiques qui les sous-tendent, notamment en ce qui concerne la formation de communautés et les implications pour la propagation de l'information et des comportements au sein des réseaux.

---
### 6. Théorie du Petit Monde (Watts & Strogatz, 1998)

#### 6.1. Contexte et Définition

La théorie du petit monde, introduite par Duncan Watts et Steven Strogatz en 1998, décrit des réseaux qui présentent simultanément :

- **Un haut degré de clustering** : Les nœuds tendent à former des groupes fortement connectés. Les amis de mes amis sont souvent aussi mes amis.
- **Une distance géodésique moyenne faible** : La plupart des nœuds peuvent être atteints en quelques étapes seulement. Malgré le clustering, le nombre d'étapes nécessaires pour atteindre n'importe quel nœud reste faible.

Ces réseaux sont appelés **réseaux du petit monde**. Réseaux sociaux humains, réseaux neuronaux, réseaux de transport.
#### 6.2. Modèle de Watts-Strogatz

- **Construction du modèle** :
  1. Commencez avec un réseau régulier où chaque nœud est connecté à \( k \) voisins les plus proches.
  2. Reconnectez aléatoirement chaque lien avec une probabilité \( p \).
  3. Pour des valeurs faibles de \( p \), le réseau passe d'un réseau régulier à un réseau du petit monde.

#### 6.3. Illustration en R

**Génération d'un réseau du petit monde**

```R
# Génération d'un réseau régulier
regular_graph <- make_lattice(length = 100, dim = 1, nei = 5, circular = TRUE)

# Génération d'un réseau du petit monde avec la réécriture de liens
small_world_graph <- rewire(regular_graph, with = keeping_degseq(niter = 500))

# Comparaison des distances moyennes et du clustering

# Clustering du réseau régulier
clustering_regular <- transitivity(regular_graph, type = "average")

# Clustering du réseau du petit monde
clustering_small_world <- transitivity(small_world_graph, type = "average")

# Distance moyenne du réseau régulier
avg_path_regular <- mean_distance(regular_graph, directed = FALSE)

# Distance moyenne du réseau du petit monde
avg_path_small_world <- mean_distance(small_world_graph, directed = FALSE)

# Affichage des résultats
cat("Réseau Régulier : Clustering =", clustering_regular, ", Distance Moyenne =", avg_path_regular, "\n")
cat("Réseau Petit Monde : Clustering =", clustering_small_world, ", Distance Moyenne =", avg_path_small_world, "\n")
```

**Explication du code :**

- **make_lattice** : Crée un réseau régulier en forme de grille.
- **rewire** : Modifie le graphe en réécrivant des liens pour introduire de l'aléatoire.
- **transitivity** : Calcule le coefficient de clustering moyen.
- **mean_distance** : Calcule la distance géodésique moyenne.

**Interprétation**

- **Comparaison des résultats** :
  - Le réseau du petit monde conserve un clustering élevé.
  - La distance moyenne est réduite par rapport au réseau régulier.
- **Conclusion** : Cela illustre le principe du réseau du petit monde.

---

#### 6.4. Implications pour la Diffusion de l'Information

**Diffusion dans les Réseaux du Petit Monde**

- **Propagation rapide** : Grâce aux courtes distances géodésiques, les informations, les rumeurs ou les épidémies peuvent se propager rapidement.
- **Rôle des raccourcis** : Les liens aléatoires agissent comme des raccourcis qui connectent des parties éloignées du réseau.

**Exemple en R : Simulation de la Diffusion**

Supposons que nous voulons simuler la diffusion d'une information dans un réseau du petit monde.

```R
# Définition d'une fonction de simulation de diffusion
simulate_diffusion <- function(graph, initial_infected, prob_spread, steps) {
  V(graph)$state <- "S"  # S pour Susceptible
  V(graph)$state[initial_infected] <- "I"  # I pour Infected
  
  for (step in 1:steps) {
    infected <- which(V(graph)$state == "I")
    for (node in infected) {
      neighbors <- neighbors(graph, node)
      for (neighbor in neighbors) {
        if (V(graph)$state[neighbor] == "S") {
          if (runif(1) < prob_spread) {
            V(graph)$state[neighbor] <- "I"
          }
        }
      }
      # Optionnel : le nœud peut devenir Récupéré (R) après une étape
      # V(graph)$state[node] <- "R"
    }
    # Comptage
    cat("Étape", step, ": Infectés =", sum(V(graph)$state == "I"), "\n")
  }
}

# Simulation sur le réseau du petit monde
simulate_diffusion(small_world_graph, initial_infected = sample(vcount(small_world_graph), 1), prob_spread = 0.1, steps = 10)
```

**Explication du code :**

- **simulate_diffusion** : Fonction qui simule la diffusion sur le graphe.
- **V(graph)$state** : Attribut pour stocker l'état de chaque nœud (Susceptible, Infecté, Récupéré).
- **runif(1) < prob_spread** : Détermine si l'infection se propage au voisin en fonction de la probabilité donnée.
- **neighbors(graph, node)** : Renvoie les voisins du nœud spécifié.

**Interprétation**

- **Observation de la propagation** : On peut voir comment le nombre de nœuds infectés évolue à chaque étape.
- **Impact de la structure du réseau** : Dans un réseau du petit monde, la propagation est généralement plus rapide que dans un réseau régulier.

**Applications Pratiques**

- **Marketing viral** : Comprendre comment une campagne peut rapidement toucher un large public.
- **Épidémiologie** : Prévoir la propagation des maladies et planifier des interventions.
- **Propagation des informations** : Analyser la diffusion des nouvelles, des rumeurs ou des fake news.
### Conclusion du Cours

**Points clés à retenir :**

- Les **distances géodésiques** et le **diamètre** sont des indicateurs essentiels de la structure d'un réseau.
- Les **réseaux du petit monde** combinent un **clustering élevé** et une **distance moyenne faible**, ce qui facilite la diffusion rapide.
- La **structure du réseau** a un impact direct sur la **vitesse** et l'**étendue** de la propagation de l'information.


---

### Lectures Recommandées pour Aller Plus Loin

- **Newman, M. E. J. (2001).** "The structure of scientific collaboration networks". *Proceedings of the National Academy of Sciences*, 98(2), 404-409.
- **Barthélemy, M. (2011).** "Spatial networks". *Physics Reports*, 499(1-3), 1-101.
- **Easley, D., & Kleinberg, J. (2010).** *Networks, Crowds, and Markets: Reasoning About a Highly Connected World*. Cambridge University Press.