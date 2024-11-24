Nous explorons la généalogie des modèles de deep learning en analyse de réseau. Ce parcours nous mènera des premiers modèles, jusqu’aux méthodes de pointe comme les **Graph Convolutional Networks (GCN)**, **Graph Attention Networks (GAT)**, **GraphSAGE** et les modèles de représentation vectorielle comme **node2vec**. Chaque avancée reflète un pas en avant pour capturer les complexités structurelles et relationnelles des réseaux sociaux, particulièrement en contexte dynamique.
# I - Méthodes et Approches Modernes en Analyse Réseau via Deep Learning

L'analyse réseau par apprentissage profond remonte aux premières tentatives d’utiliser les réseaux neuronaux sur des graphes dans les années 2000. Avec l’introduction des **Graph Neural Networks (GNN)**, cette approche a évolué vers des modèles de plus en plus sophistiqués. La genèse des méthodes de deep learning appliquées aux graphes commence avec les **GNN classiques** de **Scarselli et al. (2009)**, qui posent les bases du traitement des graphes par réseaux neuronaux, et se poursuit avec des modèles permettant des représentations de plus en plus riches et adaptées aux grands réseaux hétérogènes et dynamiques.

## 1.1  Représentation Vectorielle des Nœuds : Node2Vec

Vers 2014, **Perozzi, Al-Rfou et Skiena** introduisent **DeepWalk**, une méthode qui utilise des marches aléatoires sur le graphe pour produire des représentations vectorielles des nœuds. Cette approche s'inspire des modèles de traitement du langage naturel, notamment **Word2Vec**, en traitant les marches comme des séquences de nœuds, permettant ainsi de capturer les similarités relationnelles de premier et second ordre.

**Node2vec** (2016), proposé par **Grover et Leskovec**, améliore DeepWalk en permettant des marches aléatoires biaisées, favorisant soit l’exploration locale (en conservant la structure proche) soit globale (en se concentrant sur des nœuds plus éloignés). Cette méthode est particulièrement utile pour :
- **Analyse de similarité** (identification de nœuds proches en termes de rôle et de fonction).
- **Identification de communautés**.
- **Prédiction de liens** dans des contextes de réseaux sociaux.

Les modèles **Struct2vec** (2017) et **SDNE** (2016) sont conçus pour préserver les structures globales du réseau dans les représentations vectorielles. **Struct2vec** capture des similarités structurelles sans se baser exclusivement sur les voisinages immédiats, ce qui en fait un outil puissant pour détecter des rôles similaires dans des sous-graphes distincts. **SDNE**, quant à lui, utilise des auto-encodeurs pour intégrer des relations locales et globales, fournissant ainsi une représentation équilibrée du réseau.
### a. **Node2Vec : Marche aléatoire biaisée pour des embeddings diversifiés**

Introduit par **Grover et Leskovec en 2016**, Node2Vec s’appuie sur les bases posées par **DeepWalk** (Perozzi, Al-Rfou, et Skiena, 2014) et **Word2Vec** (Mikolov et al., 2013), méthodes qui utilisent des marches aléatoires pour créer des séquences de nœuds, similaires à des phrases dans le traitement du langage naturel. Node2Vec apporte deux innovations majeures :
   - **Marche aléatoire biaisée** : Là où DeepWalk utilisait des marches uniformes, Node2Vec introduit des **marches biaisées** avec deux paramètres de contrôle \( p \) et \( q \). Ce biais peut orienter les marches pour privilégier l’**exploration locale** (favorisant des nœuds proches, en respectant les relations immédiates) ou l’**exploration globale** (en connectant des nœuds éloignés, pour une vue d’ensemble du graphe).
   - **Flexibilité et personnalisation des embeddings** : Grâce aux paramètres \( p \) et \( q \), Node2Vec peut produire des embeddings qui capturent soit des similarités structurelles (nœuds jouant des rôles similaires, même sans connexion directe) soit des similarités topologiques (nœuds directement connectés ou proches dans le graphe).

**Algorithme Node2Vec**
1. **Initialisation** : Choix d’un point de départ et initialisation de la marche aléatoire.
2. **Étape de marche** : À chaque étape, le nœud suivant est choisi en fonction des paramètres \( p \) et \( q \) :
   - Si \( p \) est faible et \( q \) élevé, la marche reste **locale**, favorisant les liens entre nœuds proches.
   - Si \( q \) est faible et \( p \) élevé, la marche tend vers une **exploration globale**, en sautant vers des nœuds plus éloignés.
3. **Construction des embeddings** : Les séquences générées par les marches sont traitées par l’algorithme Skip-gram (comme dans Word2Vec) pour générer les embeddings des nœuds.

**Applications et Interprétation des Embeddings Node2Vec**
- **Analyse de similarité** : Les nœuds ayant des vecteurs similaires sont souvent proches en termes de fonction ou de rôle dans le réseau, même sans lien direct.
- **Identification de communautés** : Les clusters d’embeddings obtenus révèlent des groupes de nœuds jouant des rôles similaires ou ayant des interactions fréquentes.
- **Prédiction de liens** : Node2Vec est particulièrement performant pour prédire des liens potentiels en identifiant les nœuds qui devraient être connectés d’après leurs embeddings.

### b. **Struct2Vec : Préservation des Similarités Structurelles**

**Struct2Vec** (Ribeiro, Savarese, et Figueiredo, 2017) améliore la méthode Node2Vec en ne se limitant pas aux voisinages immédiats mais en capturant des similarités structurelles globales. Struct2Vec est donc particulièrement utile pour détecter des **équivalences structurelles**, où des nœuds jouent des rôles similaires dans différentes parties du réseau.

**Algorithme Struct2Vec**
1. **Construction des couches d’information** : Struct2Vec crée une série de couches représentant les nœuds et leurs voisins à différentes distances, pour capturer la structure locale et globale.
2. **Encodage hiérarchique** : Les informations de chaque couche sont encodées de manière à respecter les similarités de rôle des nœuds, et non seulement leur proximité.
3. **Génération des embeddings** : Les nœuds similaires (en termes de rôle et de position dans le réseau) reçoivent des embeddings proches, même sans connexion directe.

**Applications et Interprétation des Embeddings Struct2Vec**
- **Identification des rôles relationnels** : Struct2Vec est particulièrement adapté pour identifier des rôles relationnels comme des courtiers ou des autorités, car il capture les motifs récurrents de comportement dans des sous-graphes similaires.
- **Analyse des sous-groupes** : Struct2Vec est puissant pour révéler des sous-structures cohérentes dans des graphes sociaux, où certains groupes de nœuds peuvent jouer des rôles similaires sans nécessairement être connectés directement.

### c. **SDNE : Auto-encodeurs pour Intégration Locale et Globale**

**SDNE** (Structural Deep Network Embedding) a été développé par **Wang, Cui, et Zhu (2016)** pour capturer les structures à la fois locales et globales du réseau. SDNE repose sur des **auto-encodeurs**, un type de réseau de neurones conçu pour compresser et reconstruire des données, afin d’obtenir des représentations équilibrées du graphe.

**Algorithme SDNE**
1. **Double niveau d’encodage** : SDNE utilise une architecture d’auto-encodeurs double, où une première couche encode les relations locales (voisinage immédiat), et une seconde couche encode la structure globale du réseau.
2. **Minimisation de l’erreur de reconstruction** : SDNE s’efforce de reconstruire le graphe original tout en minimisant la perte d’information, ce qui permet de préserver les relations structurales critiques entre nœuds.
3. **Optimisation des embeddings** : Les embeddings finaux sont produits de manière à minimiser les différences locales et globales entre les nœuds, tout en capturant les rôles et les positions relatives.

**Applications et Interprétation des Embeddings SDNE**
- **Détection de communautés et de rôles complexes** : En conservant les relations locales et globales, SDNE est particulièrement adapté pour des graphes où les structures hiérarchiques ou multi-niveaux sont importantes.
- **Prédiction de liens et recommandation** : En raison de sa capacité à capturer la structure globale, SDNE est performant pour des applications comme la recommandation dans les réseaux sociaux ou les systèmes de collaboration.
### d. Synthèse Comparée : Node2Vec, Struct2Vec et SDNE

| Méthode      | Principe de Base        | Applications                         | Avantages                             | Limites                                    |
|--------------|-------------------------|--------------------------------------|---------------------------------------|--------------------------------------------|
| Node2Vec     | Marche aléatoire biaisée| Similarité, communautés, prédiction  | Adaptation locale/globale flexible    | Ne capture pas bien les similarités structurelles |
| Struct2Vec   | Similarités structurelles| Rôles, équivalence structurelle      | Adapté pour les rôles relationnels    | Plus coûteux en calcul                    |
| SDNE         | Auto-encodeurs locaux et globaux | Rôles complexes, liens, recommandation | Représentation locale et globale équilibrée | Modèle complexe, difficile à entraîner     |

Ces méthodes enrichissent considérablement l’analyse de réseaux en offrant des perspectives sur les relations et les rôles au sein de structures complexes. En combinant Node2Vec, Struct2Vec et SDNE, les chercheurs peuvent explorer différentes dimensions du réseau et obtenir des embeddings adaptés à des applications variées.

## 1.2 Les Graph Neural Networks (GNN) : Origines et Principes Fondamentaux

Les **Graph Neural Networks (GNN)**, introduits par **Scarselli et al. (2009)**, marquent une étape pionnière en adaptant les réseaux neuronaux pour les graphes. À l'origine, l’objectif était de permettre une diffusion d’information entre les nœuds, en apprenant une représentation enrichie de chaque nœud en fonction de ses voisins. Cette approche consistait à passer par plusieurs itérations où les nœuds intègrent progressivement les informations provenant de leurs voisins.

Les **GNN** sont utilisés pour :
- **Classification de nœuds** (déterminer les caractéristiques d’un nœud par ses relations).
- **Prédiction de liens** (anticipation des relations futures entre les nœuds).
- **Détection de communautés** (identifier les groupes et sous-structures dans les réseaux
Les modèles **GNN** (Graph Neural Networks), **GCN** (Graph Convolutional Networks), et **GAT** (Graph Attention Networks) représentent des approches différentes et évolutives pour l’analyse de graphes, chacun ayant des avantages spécifiques en fonction des cas d'utilisation. Ils ne se remplacent pas nécessairement, car chaque modèle apporte une réponse unique aux défis posés par les structures de graphe complexes. Cependant, certaines méthodes sont plus adaptées à certaines situations et deviennent plus populaires pour des applications spécifiques.
### a.Graph Convolutional Networks (GCN) : Convolutions sur Graphes

En 2017, les **Graph Convolutional Networks (GCN)**, introduits par **Kipf et Welling**, représentent une avancée majeure. Les GCN adaptent les réseaux convolutifs, initialement utilisés en vision par ordinateur, aux graphes. Cette approche de convolution utilise les caractéristiques des voisins d’un nœud pour enrichir sa propre représentation.

Les GCN procèdent en trois étapes principales :
1. **Aggregation** : Chaque nœud agrège les informations de ses voisins.
2. **Transformation linéaire** : Les données agrégées sont transformées via des matrices de poids.
3. **Propagation** : La propagation des informations entre les couches permet d’atteindre des nœuds plus éloignés.

Les GCN sont particulièrement efficaces pour :
- **Classification de nœuds**, en exploitant les informations topologiques.
- **Prédiction de communautés**.
- **Apprentissage semi-supervisé** : Ce modèle permet d’étiqueter un sous-ensemble de nœuds pour en inférer des étiquettes pour l’ensemble du graphe.
  
### b. Graph Attention Networks (GAT) : Mécanisme d’Attention pour Graphes

Les **Graph Attention Networks (GAT)**, proposés par **Veličković et al. (2018)**, incorporent un mécanisme d’attention, permettant de pondérer chaque voisin en fonction de son importance pour le nœud cible. Contrairement aux GCN classiques où tous les voisins sont traités de manière égale, GAT attribue un poids à chaque voisin, en fonction de son importance relative.

L’approche GAT suit plusieurs étapes :
1. **Calcul des poids d'attention** pour chaque paire de nœuds connectés.
2. **Agrégation pondérée** des informations des voisins, en prenant en compte les poids d’attention calculés.

Les GAT sont particulièrement adaptés aux réseaux où certaines connexions sont plus influentes que d’autres, et où il est important de capturer des dynamiques d’influence et de rôles.

**Limites des GAT** :
- **Coûts computationnels élevés** par rapport aux GCN car ils nécessitent des calculs d'attention pour chaque lien dans le graphe, limitant leur utilisation à des graphes de taille modérée ou petite.

### c. Complémentarité et évolution des modèles

- **Les GCN** sont encore largement utilisés, surtout pour des tâches où tous les nœuds sont disponibles au moment de l’entraînement, comme les réseaux de citation ou les réseaux biologiques bien définis.
- **Les GAT** sont privilégiés lorsque les connexions dans le réseau sont inégales en importance, comme dans les réseaux de connaissances, mais ils sont limités par les besoins computationnels plus élevés.

**Cas d'utilisation en fonction des modèles**

1. **GCN** : Classifications et tâches de propagation d’information dans des réseaux où la structure du graphe est stable et complète (ex. réseaux de citation, réseaux de transport).
2. **GAT** : Réseaux complexes avec des connexions de poids inégal, nécessitant une approche fine de l’agrégation des informations (ex. réseaux de réseaux sociaux, réseaux d'interactions en ligne).

Les GCN et GAT offrent des solutions adaptées à différents types de réseaux et problématiques. Ils ne se remplacent pas mais se complètent, permettant aux chercheurs de choisir le modèle qui correspond le mieux aux **spécificités structurelles et aux dynamiques** de leur graphe. Ainsi, chaque modèle a un champ d'application privilégié, ce qui rend utile leur coexistence dans le domaine de l’analyse des réseaux.



## 1.3 GraphSAGE : Apprentissage Inductif et Échantillonnage des Voisins

**GraphSAGE** (Graph Sample and Aggregation) est une avancée significative en **apprentissage inductif** dans les réseaux, introduite par **Hamilton, Ying, et Leskovec en 2017**. Contrairement aux **Graph Convolutional Networks (GCN)**, qui nécessitent l'accès à l'intégralité du graphe au moment de l'entraînement, GraphSAGE permet de généraliser à de nouveaux nœuds ou à des parties du graphe non vues lors de l’entraînement. Cette capacité à s’adapter aux réseaux évolutifs et à gérer les grandes structures de données en fait une approche puissante pour les réseaux dynamiques, tels que les réseaux sociaux ou professionnels en constante expansion.

### a. **Fondements Théoriques et Principe de Fonctionnement**

GraphSAGE repose sur deux principes majeurs :
1. **Échantillonnage de Voisins** : GraphSAGE utilise un sous-ensemble de voisins de chaque nœud au lieu de traiter l’ensemble complet. Cette technique permet de réduire les exigences en calcul pour les graphes massifs, tout en conservant des informations pertinentes pour chaque nœud.
   
2. **Agrégation Inductive** : Contrairement aux modèles transductifs (qui nécessitent un graphe fixe), GraphSAGE apprend des fonctions d'agrégation capables de généraliser à de nouveaux nœuds, ce qui permet de traiter des réseaux en évolution, comme ceux où de nouveaux utilisateurs ou produits apparaissent fréquemment.

### b. **Étapes et Algorithmes de GraphSAGE**

L’algorithme de GraphSAGE se compose de plusieurs étapes :

- **Échantillonnage des Voisins** : Pour chaque nœud, un nombre fixé de voisins est échantillonné. Par exemple, si on définit que chaque nœud aura 10 voisins, GraphSAGE en sélectionnera 10 de manière aléatoire, quel que soit le degré du nœud.

- **Agrégation** : GraphSAGE utilise une fonction d'agrégation (par exemple, la moyenne ou une fonction de type LSTM) pour combiner les informations provenant des voisins échantillonnés. L’agrégateur est ensuite appliqué de manière itérative couche par couche, en combinant les représentations des voisins à chaque étape.

- **Mise à Jour des Représentations** : La représentation de chaque nœud est mise à jour en fonction de celle de ses voisins échantillonnés et de sa propre représentation. Cette approche permet aux représentations finales de capturer à la fois les informations des nœuds et celles de leurs voisins directs et indirects.

### c. **Méthodes d'Agrégation dans GraphSAGE**

GraphSAGE propose plusieurs méthodes d'agrégation pour combiner les informations des voisins :
   - **Agrégation par Moyenne** : Les représentations des voisins sont simplement moyennées. Cette méthode est rapide et fournit une bonne performance dans les réseaux peu complexes.
   - **Agrégation par Pooling** : Chaque voisin passe par une couche non linéaire avant d'être combiné, ce qui peut capturer des informations plus riches.
   - **Agrégation LSTM** : Un LSTM est appliqué aux représentations des voisins, permettant de capturer des dépendances plus complexes dans les voisinages, particulièrement utile pour les réseaux avec des dépendances séquentielles.

Ces différentes méthodes d'agrégation permettent d’adapter GraphSAGE aux spécificités des données et aux exigences des applications, offrant une flexibilité appréciable dans la modélisation de réseaux.

### d. **Applications et Interprétation des Embeddings GraphSAGE**

Les embeddings produits par GraphSAGE trouvent des applications variées dans l'analyse des réseaux :

- **Prédiction de liens et de nœuds** : En raison de sa capacité à généraliser aux nœuds et aux liens non observés lors de l'entraînement, GraphSAGE est particulièrement adapté pour la prédiction de liens et la suggestion de nouveaux amis, produits, ou relations dans les réseaux sociaux ou de recommandation.
  
- **Analyse de réseaux évolutifs** : Dans les réseaux sociaux et professionnels en évolution rapide, où de nouveaux nœuds apparaissent constamment, GraphSAGE peut suivre et analyser efficacement les changements structurels sans nécessiter une reconstruction complète du modèle.

- **Systèmes de recommandation** : Dans des systèmes de recommandation, GraphSAGE permet d'intégrer facilement de nouveaux utilisateurs et articles, car les fonctions d’agrégation apprises peuvent être appliquées aux nœuds non observés précédemment.

La meilleure méthode pour obtenir un **embedding du réseau entier** dépend du type de réseau, de la quantité de données, et des objectifs de l’analyse. Voici quelques-unes des méthodes les plus courantes et adaptées pour obtenir une représentation vectorielle d’un réseau entier (embedding global) et les contextes dans lesquels elles sont les plus efficaces.

## 1.4 L'embedding de graphes : comparer

### a. **Pooling des Embeddings de Nœuds**
Une approche plus flexible consiste à obtenir des embeddings de nœuds (par exemple, avec Node2Vec, Struct2Vec, ou SDNE), puis à **agréger ces embeddings** pour obtenir un vecteur représentant le réseau entier.

- **Principe** : On commence par générer des embeddings pour chaque nœud en utilisant une méthode adaptée (par exemple, Node2Vec pour les similarités locales, ou Struct2Vec pour les similarités structurelles), puis on combine ces embeddings (par exemple, en calculant la moyenne, la somme ou en utilisant une méthode de pooling).
- **Usage** : Pratique pour les réseaux sociaux ou de communication ; permet de capturer la structure locale ou globale en fonction de la méthode choisie pour les nœuds.
- **Avantages** : Simple et adaptable ; permet une grande flexibilité dans la façon de représenter le réseau.
- **Inconvénients** : Peut manquer de finesse pour les réseaux très structurés ou avec des motifs globaux distincts.
### b. **Graph2Vec**
**Graph2Vec** est une méthode spécialement conçue pour produire des embeddings de réseaux entiers. Elle s'inspire de **Doc2Vec** pour représenter les réseaux en utilisant les sous-structures locales (par exemple, des petits sous-graphes ou motifs) comme des "phrases" qui forment un "document" représentant le réseau entier.

- **Principe** : Graph2Vec extrait des sous-structures locales du réseau (comme des chemins de longueur fixe ou des motifs comme les triangles) et utilise ces sous-structures comme caractéristiques du réseau. L’algorithme génère ensuite un embedding en traitant le réseau comme un ensemble de motifs.
- **Usage** : Très utile pour les réseaux qui peuvent être bien représentés par leurs motifs locaux (réseaux biologiques, moléculaires, ou de réseaux d'interaction).
- **Avantages** : Convient aux réseaux de taille moyenne à grande ; permet de capturer la structure locale et offre une interprétation plus riche pour les réseaux ayant des motifs distincts.
- **Inconvénients** : Peut être moins adapté pour les réseaux sans motifs ou pour les très grands réseaux.

### c. **Diffusion Embedding**
Les méthodes d'embedding basées sur la **diffusion** (comme **Diff2Vec**) calculent des embeddings en simulant une diffusion d’information dans le réseau, en capturant ainsi des aspects globaux de la structure du réseau.

- **Principe** : La diffusion est simulée à partir de chaque nœud pour capturer sa position relative dans le réseau global. La matrice de diffusion est ensuite factorisée pour générer un embedding global.
- **Usage** : Recommandé pour des réseaux où l’information a tendance à se propager de manière complexe, comme dans les réseaux de citations ou de communication.
- **Avantages** : Capture efficacement les similarités globales ; particulièrement utile pour des réseaux de type monde petit, où la diffusion permet de saisir les interactions à travers le réseau entier.
- **Inconvénients** : Peut être coûteux en termes de calcul pour des réseaux très larges ; nécessite de la mémoire pour la diffusion.
### d. **Graph Neural Networks (GNN) avec Pooling**
Les **Graph Neural Networks** comme les **Graph Convolutional Networks (GCN)** ou les **Graph Attention Networks (GAT)** peuvent être adaptés pour générer un embedding de réseau entier en utilisant une étape de **pooling global**

- **Principe** : Un GNN est entraîné pour apprendre une représentation du réseau dans son ensemble en appliquant un pooling global des représentations de couches finales. Cela permet de capturer des informations d’échelle locale et globale du réseau.
- **Usage** : Pertinent pour des réseaux complexes où les attributs de nœuds ou les relations entre nœuds doivent être intégrés dans la représentation finale ; particulièrement efficace dans les réseaux de connaissances ou les réseaux multi-attributs.
- **Avantages** : Très flexible et performant ; permet d’intégrer des informations de diverses couches (locale à globale).
- **Inconvénients** : Peut être coûteux en termes de ressources, surtout pour des réseaux denses ; nécessite une grande quantité de données d'entraînement.

### e. **Embeddings Basés sur des Statistiques Globales (Graph Fingerprinting)**
Une méthode plus classique, mais toujours utile, consiste à calculer des **statistiques globales** pour caractériser le réseau entier, créant ainsi un vecteur descriptif.

- **Principe** : Cette approche utilise des mesures globales (par exemple, le degré moyen, le coefficient de clustering, la centralité moyenne) pour créer un vecteur statistique qui représente le réseau.
- **Usage** : Très utile pour une comparaison rapide entre réseaux ; par exemple, pour comparer des réseaux de différentes structures (réseaux aléatoires vs. réseaux à échelle).
- **Avantages** : Simple et rapide ; nécessite peu de ressources computationnelles.
- **Inconvénients** : Limité en précision ; ne capture pas toujours les motifs locaux importants.

### Comparaison des Méthodes et Recommandations

| Méthode                    | Avantages                                                                                  | Limites                                                                | Utilisation Idéale                          |
|----------------------------|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------|---------------------------------------------|
| **Graph2Vec**              | Captures bien les motifs locaux ; adapté aux réseaux moyens à grands                       | Moins adapté pour les très grands réseaux                              | Réseaux avec motifs récurrents             |
| **Diffusion Embedding**    | Captures les similarités globales ; efficace pour les réseaux de diffusion                 | Coûteux pour les réseaux très larges                                   | Réseaux de diffusion                       |
| **Pooling des Embeddings de Nœuds** | Flexible ; permet de capturer des structures locales et globales               | Manque de précision dans les réseaux très structurés                   | Réseaux sociaux diversifiés                |
| **GNN avec Pooling**       | Flexibilité ; performances accrues avec les informations de nœuds et relations             | Nécessite beaucoup de calcul et d'entraînement                         | Réseaux complexes et multi-attributs       |
| **Graph Fingerprinting**   | Rapide et facile ; bonne vue d’ensemble                                                    | Ne capture pas les motifs locaux                                       | Comparaison rapide entre grands réseaux    |

### Recommandation Générale
- **Pour les réseaux de taille moyenne** et ayant une structure complexe : **Graph2Vec** ou un **pooling d’embeddings de nœuds** est souvent suffisant.
- **Pour les très grands réseaux évolutifs** : Les méthodes inductives comme **GraphSAGE** ou les **diffusion embeddings** sont préférables.
- **Pour une analyse fine des rôles** dans des réseaux denses et complexes : Utiliser **GNN avec pooling**.

Chaque méthode a donc ses forces et ses faiblesses. Pour des analyses avancées, il est souvent bénéfique de combiner plusieurs méthodes et de comparer les résultats afin de bien saisir les différentes facettes de la structure du réseau.

# II Methode R et Python dans l'analyse deeplearning des graphes

## 2.1  Représentation Vectorielle des Nœuds : Node2Vec

### a. Node2Vec

Voici un code R détaillé qui met en œuvre l'algorithme Node2Vec sur un réseau de citation web, en utilisant les dataframes `nodes` et `links`. Ce code utilise la bibliothèque `reticulate` pour intégrer du code Python, notamment pour utiliser l'implémentation Node2Vec disponible en Python.

```R
Je vais proposer une version optimisée du code avec des commentaires détaillés expliquant les améliorations :

```R
# Optimisation 1 : Chargement efficace des packages avec pacman
if (!require("pacman")) install.packages("pacman")
pacman::p_load(
  data.table,  # Pour fread, plus rapide que read.csv
  reticulate,
  igraph,
  Rtsne,
  ggplot2,
  dplyr,
  future      # Pour la parallélisation
)

# Optimisation 2 : Configuration de la parallélisation
future::plan(future::multisession)

# Optimisation 3 : Lecture plus rapide des fichiers avec data.table
nodes <- fread("nodes.csv")
links <- fread("links.csv")

# Optimisation 4 : Conversion des types de données plus efficace
links <- links %>%
  mutate(across(c(source, target), as.integer))

# Import Python avec gestion des erreurs
tryCatch({
  pandas <- import("pandas")
  nx <- import("networkx")
  node2vec <- import("node2vec")
}, error = function(e) {
  stop("Erreur lors de l'importation des modules Python:", e$message)
})

# Optimisation 5 : Fonction pour créer et entraîner Node2Vec
create_and_train_node2vec <- function(G, p, q, dimensions = 64L) {
  node2vec_instance <- node2vec$Node2Vec(
    G,
    dimensions = dimensions,
    walk_length = 30L,
    num_walks = 200L,
    workers = parallel::detectCores() - 1,  # Utilisation optimale des cores
    p = p,
    q = q
  )
  
  model <- node2vec_instance$fit(
    window = 10L,
    min_count = 1L,
    batch_words = 4L
  )
  
  return(model)
}

# Optimisation 6 : Fonction pour extraire et transformer les embeddings
process_embeddings <- function(model, nodes) {
  embedding_keys <- as.integer(model$wv$index_to_key)
  embedding_matrix <- model$wv$vectors
  
  # Création du dataframe d'embeddings avec data.table
  embedding_df <- data.table(
    node_id = embedding_keys,
    as.data.table(embedding_matrix)
  )
  
  # t-SNE avec gestion des erreurs
  tryCatch({
    tsne_results <- Rtsne(
      embedding_df[, -1],
      dims = 2,
      perplexity = 30,
      verbose = FALSE,
      max_iter = 500
    )
    
    embedding_df[, c("tsne_x", "tsne_y") := as.data.table(tsne_results$Y)]
  }, error = function(e) {
    warning("Erreur lors du t-SNE:", e$message)
  })
  
  return(embedding_df)
}

# Optimisation 7 : Fonction de visualisation améliorée
create_visualization <- function(nodes_embeddings, title) {
  ggplot(nodes_embeddings, 
         aes(x = tsne_x, y = tsne_y, color = typeacteur, shape = opinionpolitique)) +
    geom_point(size = 1) +  # Taille réduite pour meilleure performance
    theme_minimal() +
    theme(
      text = element_text(size = 12),
      plot.title = element_text(hjust = 0.5)
    ) +
    labs(title = title) +
    scale_color_brewer(palette = "Set3")  # Meilleure palette de couleurs
}

# Exécution principale
G <- nx$from_pandas_edgelist(r_to_py(links), 
                            source = 'source', 
                            target = 'target', 
                            edge_attr = 'weight', 
                            create_using = nx$DiGraph())

# Premier modèle (p=1, q=1)
model1 <- create_and_train_node2vec(G, p = 1, q = 1)
embeddings1 <- process_embeddings(model1, nodes)
nodes_embeddings1 <- merge(nodes, embeddings1, by.x = 'id', by.y = 'node_id')

# Deuxième modèle (p=0.5, q=2)
model2 <- create_and_train_node2vec(G, p = 0.5, q = 2)
embeddings2 <- process_embeddings(model2, nodes)
nodes_embeddings2 <- merge(nodes, embeddings2, by.x = 'id', by.y = 'node_id')

# Visualisations
p1 <- create_visualization(nodes_embeddings1, "Node2Vec Embeddings (p=1, q=1)")
p2 <- create_visualization(nodes_embeddings2, "Node2Vec Embeddings (p=0.5, q=2)")

# Optimisation 8 : Sauvegarde des résultats
fwrite(nodes_embeddings1, "embeddings_p1q1.csv")
fwrite(nodes_embeddings2, "embeddings_p0.5q2.csv")
```

**Explications détaillées :**

1. **Chargement des bibliothèques** : Le code commence par charger les bibliothèques nécessaires, y compris `reticulate` pour interfacer avec Python.

2. **Génération des données d'exemple** : Des dataframes `nodes` et `links` sont créés pour simuler un réseau de citation web avec des variables catégorielles telles que `typeacteur` et `opinionpolitique`.

3. **Exportation des données** : Les dataframes sont écrits dans des fichiers CSV pour être utilisés en Python.

4. **Interfaçage avec Python** :
   - Importation des modules Python `pandas`, `networkx` et `node2vec`.
   - Lecture de la liste des arêtes (`edgelist.csv`) en Python et création du graphe orienté `G` avec `networkx`.

5. **Initialisation et entraînement de Node2Vec** :
   - Création d'une instance de Node2Vec avec des paramètres spécifiques pour `p` et `q`.
   - Entraînement du modèle pour générer les embeddings des nœuds.

6. **Extraction et traitement des embeddings** :
   - Extraction des vecteurs d'embedding depuis le modèle entraîné.
   - Conversion des embeddings en data frame R et association avec les identifiants de nœuds.

7. **Visualisation des embeddings** :
   - Réduction de dimension avec t-SNE pour visualiser les embeddings en 2D.
   - Fusion des résultats t-SNE avec les attributs des nœuds pour une visualisation enrichie.
   - Utilisation de `ggplot2` pour créer des graphiques montrant la distribution des nœuds selon leurs embeddings, colorés par `typeacteur` et marqués par `opinionpolitique`.

8. **Expérimentation avec les paramètres `p` et `q`** :
   - Répétition du processus avec des valeurs différentes de `p` et `q` pour observer l'impact sur les embeddings et leur interprétation.

9. **Clustering des embeddings** :
   - Application de l'algorithme k-means sur les embeddings pour identifier des communautés ou des groupes de nœuds similaires.
   - Visualisation des clusters résultants pour interpréter les relations entre les nœuds.

**Applications possibles :**

- **Analyse de similarité** : En examinant les distances entre les embeddings, on peut identifier quels sites web ont des rôles ou des opinions politiques similaires.
- **Identification de communautés** : Le clustering permet de découvrir des groupes de sites web qui interagissent fréquemment ou qui jouent des rôles similaires dans le réseau.
- **Prédiction de liens** : En utilisant les embeddings, il est possible de prédire quels sites web pourraient établir des liens à l'avenir, sur la base de leur proximité dans l'espace des embeddings.

Ce code fournit une implémentation complète de l'algorithme Node2Vec en R, tout en exploitant la puissance des bibliothèques Python via `reticulate`. Les commentaires détaillés et les étapes expliquées permettent de comprendre et de reproduire le processus pour des analyses avancées de graphes dans le domaine des sciences sociales computationnelles.

### b. Struct2Vec


```R
#' Configuration initiale et chargement des dépendances
#' @description Configure l'environnement et charge les bibliothèques nécessaires
setup_environment <- function() {
  required_r_packages <- c("reticulate", "ggplot2", "Rtsne")
  required_py_packages <- c("networkx", "karateclub", "numpy")
  
  # Installation des packages R manquants
  for(pkg in required_r_packages) {
    if(!require(pkg, character.only = TRUE)) {
      install.packages(pkg)
      library(pkg, character.only = TRUE)
    }
  }
  
  # Installation des packages Python manquants
  for(pkg in required_py_packages) {
    tryCatch({
      reticulate::py_install(pkg, pip = TRUE)
    }, error = function(e) {
      message(sprintf("Erreur lors de l'installation de %s: %s", pkg, e$message))
    })
  }
  
  # Import des modules Python
  list(
    nx = reticulate::import("networkx"),
    kc = reticulate::import("karateclub"),
    np = reticulate::import("numpy")
  )
}

#' Lecture et préparation des données
#' @param nodes_path Chemin vers le fichier nodes.csv
#' @param links_path Chemin vers le fichier links.csv
#' @return Liste contenant les données préparées
load_and_prepare_data <- function(nodes_path, links_path) {
  tryCatch({
    nodes <- read.csv(nodes_path, stringsAsFactors = FALSE)
    links <- read.csv(links_path, stringsAsFactors = FALSE)
    
    # Conversion en format Python
    py_links <- reticulate::r_to_py(links)
    py_links$source <- py_links$source$astype("int")
    py_links$target <- py_links$target$astype("int")
    
    list(nodes = nodes, py_links = py_links)
  }, error = function(e) {
    stop(sprintf("Erreur lors de la lecture des données: %s", e$message))
  })
}

#' Création et entraînement du modèle Struct2Vec
#' @param G Graphe NetworkX
#' @param dimensions Nombre de dimensions pour les embeddings
#' @param workers Nombre de workers pour le parallélisme
#' @return Matrice des embeddings
train_struct2vec <- function(G, dimensions = 64L, workers = 4L) {
  tryCatch({
    struc2vec_model <- kc$Struc2Vec(dimensions = dimensions, workers = workers)
    struc2vec_model$fit(G)
    embeddings <- struc2vec_model$get_embedding()
    
    # Conversion en dataframe R avec IDs
    embedding_df <- as.data.frame(embeddings)
    embedding_df$node_id <- as.integer(rownames(embeddings))
    embedding_df
  }, error = function(e) {
    stop(sprintf("Erreur lors de l'entraînement du modèle: %s", e$message))
  })
}

#' Application de t-SNE et visualisation
#' @param embedding_df Dataframe des embeddings
#' @param nodes Données des nœuds
#' @param perplexity Paramètre de perplexité pour t-SNE
#' @return Plot ggplot2
create_visualization <- function(embedding_df, nodes, perplexity = 30) {
  # t-SNE
  tsne_results <- Rtsne(embedding_df[, 1:(ncol(embedding_df)-1)], 
                        dims = 2,
                        perplexity = perplexity,
                        verbose = FALSE,
                        max_iter = 500)
  
  # Préparation des données pour la visualisation
  viz_df <- data.frame(
    node_id = embedding_df$node_id,
    tsne_x = tsne_results$Y[,1],
    tsne_y = tsne_results$Y[,2]
  )
  
  # Fusion avec les données des nœuds
  nodes_embeddings <- merge(nodes, viz_df,
                          by.x = 'id',
                          by.y = 'node_id',
                          all.x = TRUE)
  
  # Création du plot
  ggplot(nodes_embeddings,
         aes(x = tsne_x,
             y = tsne_y,
             color = typeacteur,
             shape = opinionpolitique)) +
    geom_point(size = 3) +
    theme_minimal() +
    labs(title = "Visualisation t-SNE des embeddings Struct2Vec") +
    theme(
      plot.title = element_text(hjust = 0.5, size = 14),
      legend.position = "right",
      legend.title = element_text(size = 10),
      legend.text = element_text(size = 8)
    )
}

#' Fonction principale
#' @description Exécute l'ensemble du pipeline d'analyse
main <- function() {
  # Configuration de l'environnement
  py_modules <- setup_environment()
  
  # Chargement des données
  data <- load_and_prepare_data("nodes.csv", "links.csv")
  
  # Création du graphe
  G <- py_modules$nx$from_pandas_edgelist(
    data$py_links,
    source = 'source',
    target = 'target',
    edge_attr = 'weight',
    create_using = py_modules$nx$Graph()
  )
  
  # Entraînement du modèle et obtention des embeddings
  embedding_df <- train_struct2vec(G)
  
  # Création et sauvegarde de la visualisation
  plot <- create_visualization(embedding_df, data$nodes)
  
  # Sauvegarde du plot
  ggsave("struct2vec_visualization.pdf", plot, width = 10, height = 8)
  
  return(plot)
}

# Exécution du programme
set.seed(42) # Pour la reproductibilité
main()
```
1. **Modularité** :
   - Le code est divisé en fonctions distinctes avec des responsabilités claires
   - Chaque fonction gère une partie spécifique du pipeline de traitement
   - Les fonctions sont documentées avec des commentaires explicatifs

2. **Gestion des erreurs** :
   - Utilisation de `tryCatch` pour gérer les erreurs potentielles
   - Messages d'erreur explicites pour faciliter le débogage

3. **Performance** :
   - Optimisation de la gestion de la mémoire
   - Paramètres configurables pour t-SNE et Struct2Vec
   - Utilisation efficace des ressources système

4. **Reproductibilité** :
   - Ajout de `set.seed()` pour garantir des résultats reproductibles
   - Configuration explicite des paramètres importants

5. **Visualisation améliorée** :
   - Thème ggplot2 personnalisé pour une meilleure lisibilité
   - Options de personnalisation des graphiques
   - Sauvegarde automatique des visualisations

6. **Flexibilité** :
   - Paramètres configurables pour les différentes étapes du processus
   - Facilité d'adaptation à différents jeux de données
   - Possibilité d'ajuster les paramètres de visualisation

7. **Documentation** :
   - Documentation claire des fonctions avec le format Roxygen
   - Description des paramètres et des valeurs de retour
   - Explications des étapes importantes du processus

### c.SDNE

Voici une version optimisée du code avec une meilleure structure et des fonctionnalités améliorées :

```R
#' Configuration de l'environnement et des dépendances
#' @description Initialise l'environnement R et Python avec les packages nécessaires
#' @return Liste des modules Python importés
setup_environment <- function() {
  required_r_packages <- c("reticulate", "ggplot2", "Rtsne")
  required_py_packages <- c("networkx", "karateclub", "numpy")
  
  # Installation et chargement des packages R
  for(pkg in required_r_packages) {
    if(!require(pkg, character.only = TRUE)) {
      install.packages(pkg)
      library(pkg, character.only = TRUE)
    }
  }
  
  # Installation des packages Python
  tryCatch({
    reticulate::py_install(required_py_packages, pip = TRUE)
  }, error = function(e) {
    stop(sprintf("Erreur d'installation Python: %s", e$message))
  })
  
  # Import des modules Python
  list(
    nx = reticulate::import("networkx"),
    kc = reticulate::import("karateclub")
  )
}

#' Chargement et préparation des données
#' @param nodes_path Chemin vers le fichier des nœuds
#' @param links_path Chemin vers le fichier des liens
#' @return Liste contenant les données préparées
prepare_data <- function(nodes_path, links_path) {
  tryCatch({
    # Lecture des fichiers CSV
    nodes <- read.csv(nodes_path, stringsAsFactors = FALSE)
    links <- read.csv(links_path, stringsAsFactors = FALSE)
    
    # Conversion pour Python
    py_links <- reticulate::r_to_py(links)
    py_links$source <- py_links$source$astype("int")
    py_links$target <- py_links$target$astype("int")
    
    list(nodes = nodes, py_links = py_links)
  }, error = function(e) {
    stop(sprintf("Erreur de chargement des données: %s", e$message))
  })
}

#' Configuration et entraînement du modèle SDNE
#' @param G Graphe NetworkX
#' @param params Liste des paramètres du modèle
#' @return Matrice des embeddings
train_sdne <- function(G, params = list()) {
  # Paramètres par défaut
  default_params <- list(
    dimensions = 64L,
    hidden_size = c(256L, 128L),
    epochs = 50L,
    learning_rate = 0.01,
    beta = 5,
    alpha = 1e-5
  )
  
  # Fusion des paramètres par défaut avec les paramètres fournis
  params <- modifyList(default_params, params)
  
  tryCatch({
    # Création et entraînement du modèle
    sdne_model <- kc$SDNE(
      dimensions = params$dimensions,
      hidden_size = params$hidden_size,
      epochs = params$epochs,
      learning_rate = params$learning_rate,
      beta = params$beta,
      alpha = params$alpha
    )
    
    sdne_model$fit(G)
    embeddings <- sdne_model$get_embedding()
    
    # Conversion en dataframe R
    embedding_df <- as.data.frame(embeddings)
    embedding_df$node_id <- as.integer(rownames(embeddings))
    
    embedding_df
  }, error = function(e) {
    stop(sprintf("Erreur d'entraînement SDNE: %s", e$message))
  })
}

#' Application de t-SNE et création de la visualisation
#' @param embedding_df Dataframe des embeddings
#' @param nodes Données des nœuds
#' @param tsne_params Paramètres pour t-SNE
#' @return Plot ggplot2
create_visualization <- function(embedding_df, nodes, tsne_params = list()) {
  # Paramètres par défaut pour t-SNE
  default_tsne_params <- list(
    dims = 2,
    perplexity = 30,
    verbose = FALSE,
    max_iter = 500
  )
  
  tsne_params <- modifyList(default_tsne_params, tsne_params)
  
  # Application de t-SNE
  tsne_results <- Rtsne(
    embedding_df[, 1:(ncol(embedding_df)-1)],
    dims = tsne_params$dims,
    perplexity = tsne_params$perplexity,
    verbose = tsne_params$verbose,
    max_iter = tsne_params$max_iter
  )
  
  # Préparation des données pour la visualisation
  viz_df <- data.frame(
    node_id = embedding_df$node_id,
    tsne_x = tsne_results$Y[,1],
    tsne_y = tsne_results$Y[,2]
  )
  
  # Fusion avec les données des nœuds
  nodes_embeddings <- merge(
    nodes,
    viz_df,
    by.x = 'id',
    by.y = 'node_id',
    all.x = TRUE
  )
  
  # Création du plot
  ggplot(nodes_embeddings,
         aes(x = tsne_x,
             y = tsne_y,
             color = typeacteur,
             shape = opinionpolitique)) +
    geom_point(size = 3, alpha = 0.7) +
    theme_minimal() +
    labs(
      title = "Visualisation t-SNE des embeddings SDNE",
      x = "t-SNE dimension 1",
      y = "t-SNE dimension 2"
    ) +
    theme(
      plot.title = element_text(hjust = 0.5, size = 14),
      legend.position = "right",
      legend.title = element_text(size = 10),
      legend.text = element_text(size = 8)
    ) +
    scale_color_brewer(palette = "Set3")
}

#' Fonction principale d'exécution
#' @description Exécute l'ensemble du pipeline d'analyse
#' @param nodes_path Chemin vers le fichier des nœuds
#' @param links_path Chemin vers le fichier des liens
#' @param save_plot Booléen indiquant si le plot doit être sauvegardé
main <- function(nodes_path = "nodes.csv",
                links_path = "links.csv",
                save_plot = TRUE) {
  
  # Configuration de l'environnement
  py_modules <- setup_environment()
  
  # Chargement des données
  data <- prepare_data(nodes_path, links_path)
  
  # Création du graphe
  G <- py_modules$nx$from_pandas_edgelist(
    data$py_links,
    source = 'source',
    target = 'target',
    edge_attr = 'weight',
    create_using = py_modules$nx$Graph()
  )
  
  # Entraînement SDNE et obtention des embeddings
  embedding_df <- train_sdne(G)
  
  # Création de la visualisation
  plot <- create_visualization(embedding_df, data$nodes)
  
  # Sauvegarde optionnelle du plot
  if(save_plot) {
    ggsave("sdne_visualization.pdf", plot, width = 10, height = 8)
  }
  
  return(plot)
}

# Exécution avec gestion des erreurs
tryCatch({
  set.seed(42) # Pour la reproductibilité
  result <- main()
  print(result)
}, error = function(e) {
  message("Une erreur est survenue lors de l'exécution:")
  message(e$message)
})
```

**Améliorations principales :**

1. **Structure modulaire** :
   - Fonctions séparées pour chaque étape du processus
   - Meilleure organisation du code
   - Facilité de maintenance et de réutilisation

2. **Gestion des erreurs** :
   - Utilisation systématique de `tryCatch`
   - Messages d'erreur détaillés
   - Robustesse accrue

3. **Paramétrage flexible** :
   - Paramètres configurables pour SDNE et t-SNE
   - Valeurs par défaut raisonnables
   - Possibilité de personnalisation

4. **Visualisation améliorée** :
   - Meilleure esthétique avec `theme_minimal`
   - Palette de couleurs optimisée
   - Labels et légendes plus clairs

5. **Documentation** :
   - Documentation complète des fonctions
   - Description des paramètres
   - Commentaires explicatifs

6. **Bonnes pratiques** :
   - Gestion de la reproductibilité avec `set.seed`
   - Sauvegarde optionnelle des résultats
   - Code plus propre et maintenable

Cette version optimisée offre une meilleure expérience utilisateur et une plus grande flexibilité pour les analyses futures, tout en maintenant la rigueur nécessaire pour les analyses en sciences sociales et politiques.

## 2.2 Les Graph Neural Networks (GNN) : Origines et Principes Fondamentaux
### a. GCN

```R
# Charger les bibliothèques nécessaires
library(reticulate)
library(ggplot2)
library(Rtsne)

# Installer les paquets Python requis
py_install(c("tensorflow", "spektral", "numpy", "networkx", "pandas"), pip=TRUE)

# Lire les données depuis les fichiers CSV
nodes <- read.csv("nodes.csv", stringsAsFactors=FALSE)
links <- read.csv("links.csv", stringsAsFactors=FALSE)

# Importer les modules Python nécessaires
tf <- import("tensorflow")
np <- import("numpy")
spektral <- import("spektral")
nx <- import("networkx")
pd <- import("pandas")

# Convertir les dataframes R en dataframes pandas
py_nodes <- pd$DataFrame(nodes)
py_links <- pd$DataFrame(links)

# Créer le graphe en Python avec NetworkX
G <- nx$from_pandas_edgelist(py_links, source='source', target='target', edge_attr='weight', create_using=nx$Graph())

# Générer la matrice d'adjacence
A = nx$adjacency_matrix(G)
A = A$toarray()

# Préparer les caractéristiques des nœuds (features)
# Ici, nous utilisons un encodage one-hot des attributs catégoriels
typeacteur_dummies <- pd$get_dummies(py_nodes$typeacteur)
opinionpolitique_dummies <- pd$get_dummies(py_nodes$opinionpolitique)
features_df <- pd$concat(list(typeacteur_dummies, opinionpolitique_dummies), axis=1)
features <- features_df$values

# Convertir en tenseurs TensorFlow
A_tf <- tf$convert_to_tensor(A, dtype=tf$float32)
X_tf <- tf$convert_to_tensor(features, dtype=tf$float32)

# Construire le modèle GCN avec Keras et Spektral
input_features <- tf$keras$Input(shape=dim(X_tf)[2])
output = spektral$layers$GCNConv(16L, activation='relu')$call(list(input_features, A_tf))
output = spektral$layers$GCNConv(16L, activation='relu')$call(list(output, A_tf))
model <- tf$keras$Model(inputs=input_features, outputs=output)

# Compiler le modèle
model$compile(optimizer='adam', loss='categorical_crossentropy', metrics='accuracy')

# Simuler des étiquettes pour l'apprentissage supervisé
set.seed(123)
num_classes <- 3L
labels <- np$random$randint(0L, num_classes, dim(X_tf)[1])
labels_onehot <- tf$one_hot(labels, num_classes)

# Entraîner le modèle
model$fit(X_tf, labels_onehot, epochs=100L, batch_size=32L, verbose=0L)

# Extraire les embeddings
embedding_model <- tf$keras$Model(inputs=input_features, outputs=output)
embeddings <- embedding_model$predict(X_tf)

# Convertir les embeddings en data frame R
embeddings_df <- as.data.frame(embeddings)
embeddings_df$node_id <- nodes$id

# Réaliser une réduction de dimension avec t-SNE
tsne_results <- Rtsne(embeddings_df[, 1:16], dims=2, perplexity=5, verbose=FALSE, max_iter=500)

embeddings_df$tsne_x <- tsne_results$Y[,1]
embeddings_df$tsne_y <- tsne_results$Y[,2]

# Fusionner les embeddings avec les données de nœuds
nodes_embeddings <- merge(nodes, embeddings_df[, c('node_id', 'tsne_x', 'tsne_y')], by.x='id', by.y='node_id', all.x=TRUE)

# Visualiser les embeddings avec ggplot2
ggplot(nodes_embeddings, aes(x=tsne_x, y=tsne_y, color=typeacteur, shape=opinionpolitique)) +
  geom_point(size=3) +
  theme_minimal() +
  labs(title="Visualisation t-SNE des embeddings GCN")
```


**Génération de la matrice d'adjacence**

```R
# Générer la matrice d'adjacence
A = nx$adjacency_matrix(G)
A = A$toarray()
```

- **Explication :**
  - `nx$adjacency_matrix(G)` génère une matrice creuse (sparse matrix) représentant les connexions entre les nœuds.
  - `A$toarray()` convertit la matrice creuse en une matrice NumPy dense.

**Exemple de matrice d'adjacence `A` :**

Pour notre exemple avec 5 nœuds (id de 0 à 4), la matrice d'adjacence `A` sera une matrice 5x5 :

```
A = [[0, 1, 0, 1, 0],
     [1, 0, 1, 0, 0],
     [0, 1, 0, 0, 1],
     [1, 0, 0, 0, 1],
     [0, 0, 1, 1, 0]]
```

- **Interprétation :**
  - `A[i][j] = 1` signifie qu'il y a une connexion entre le nœud `i` et le nœud `j`.
  - Par exemple, `A[0][1] = 1` indique une connexion entre le nœud 0 et le nœud 1.

**Préparation des caractéristiques des nœuds (features)**

```R
# Ici, nous utilisons un encodage one-hot des attributs catégoriels
typeacteur_dummies <- pd$get_dummies(py_nodes$typeacteur)
opinionpolitique_dummies <- pd$get_dummies(py_nodes$opinionpolitique)
features_df <- pd$concat(list(typeacteur_dummies, opinionpolitique_dummies), axis=1)
features <- features_df$values
```

- **Explication :**
  - **Encodage one-hot** : Convertit les variables catégorielles en variables numériques binaires.
  - **`pd$get_dummies`** : Crée des colonnes binaires pour chaque catégorie.

**Exemple d'encodage one-hot :**

**Variables catégorielles :**

- `typeacteur` : ['gouvernement', 'média', 'entreprise', 'ONG']
- `opinionpolitique` : ['gauche', 'centre', 'droite']

**Encodage :**

- **`typeacteur_dummies`**

| gouvernement | média | entreprise | ONG |
|--------------|-------|------------|-----|
| 1            | 0     | 0          | 0   |
| 0            | 1     | 0          | 0   |
| 0            | 0     | 1          | 0   |
| 0            | 0     | 0          | 1   |
| 0            | 1     | 0          | 0   |

- **`opinionpolitique_dummies`**

| gauche | centre | droite |
|--------|--------|--------|
| 1      | 0      | 0      |
| 0      | 1      | 0      |
| 0      | 0      | 1      |
| 1      | 0      | 0      |
| 0      | 0      | 1      |

- **`features_df`** (concaténation des deux)

| gouvernement | média | entreprise | ONG | gauche | centre | droite |
|--------------|-------|------------|-----|--------|--------|--------|
| 1            | 0     | 0          | 0   | 1      | 0      | 0      |
| 0            | 1     | 0          | 0   | 0      | 1      | 0      |
| 0            | 0     | 1          | 0   | 0      | 0      | 1      |
| 0            | 0     | 0          | 1   | 1      | 0      | 0      |
| 0            | 1     | 0          | 0   | 0      | 0      | 1      |

- **`features`** : Matrice NumPy des valeurs.

**Interprétation :**

- Chaque nœud est représenté par un vecteur binaire indiquant sa catégorie pour chaque attribut.
- Par exemple, le nœud 0 (id=0) a pour vecteur de caractéristiques :
  - `[1, 0, 0, 0, 1, 0, 0]` correspondant à :
    - `gouvernement` : 1
    - `média` : 0
    - `entreprise` : 0
    - `ONG` : 0
    - `gauche` : 1
    - `centre` : 0
    - `droite` : 0

**Conversion en tenseurs TensorFlow**

```R
# Convertir en tenseurs TensorFlow
A_tf <- tf$convert_to_tensor(A, dtype=tf$float32)
X_tf <- tf$convert_to_tensor(features, dtype=tf$float32)
```

- **Explication :**
  - **`A_tf`** : Tenseur représentant la matrice d'adjacence, utilisé pour guider les opérations de convolution sur le graphe.
  - **`X_tf`** : Tenseur contenant les caractéristiques des nœuds, servant d'entrée au modèle GCN.

**Exemple de `A_tf` et `X_tf` :**

- **`A_tf`** : Même contenu que la matrice `A`, mais sous forme de tenseur TensorFlow de type `float32`.

- **`X_tf`** : Tenseur de dimension `(nombre_de_nœuds, nombre_de_caractéristiques)`.

  - Dans notre exemple :
    - `nombre_de_nœuds` : 5
    - `nombre_de_caractéristiques` : 7 (4 pour `typeacteur` + 3 pour `opinionpolitique`)

- **Contenu de `X_tf` :**

```
[[1., 0., 0., 0., 1., 0., 0.],  # Nœud 0
 [0., 1., 0., 0., 0., 1., 0.],  # Nœud 1
 [0., 0., 1., 0., 0., 0., 1.],  # Nœud 2
 [0., 0., 0., 1., 1., 0., 0.],  # Nœud 3
 [0., 1., 0., 0., 0., 0., 1.]]  # Nœud 4
```

**Récapitulatif des données préparées**

- **Matrice d'adjacence `A_tf` :**

```
[[0., 1., 0., 1., 0.],
 [1., 0., 1., 0., 0.],
 [0., 1., 0., 0., 1.],
 [1., 0., 0., 0., 1.],
 [0., 0., 1., 1., 0.]]
```

- **Caractéristiques des nœuds `X_tf` :**

```
[[1., 0., 0., 0., 1., 0., 0.],
 [0., 1., 0., 0., 0., 1., 0.],
 [0., 0., 1., 0., 0., 0., 1.],
 [0., 0., 0., 1., 1., 0., 0.],
 [0., 1., 0., 0., 0., 0., 1.]]
```

**Le Modele GCN**

concentrons-nous sur les lignes de code qui construisent le modèle GCN et expliquons-les en détail pour des étudiants n'ayant jamais fait de deep learning.

```R
# Importer les modules Python nécessaires
tf <- import("tensorflow")
spektral <- import("spektral")

# Construire le modèle GCN

# Définir la couche d'entrée
input_features <- tf$keras$Input(shape=dim(X_tf)[2])

# Première couche de convolution sur graphe
output <- spektral$layers$GCNConv(16L, activation='relu')$call(list(input_features, A_tf))

# Deuxième couche de convolution sur graphe
output <- spektral$layers$GCNConv(16L, activation='relu')$call(list(output, A_tf))

# Définir le modèle final
model <- tf$keras$Model(inputs=input_features, outputs=output)
```

**Définition de la couche d'entrée :**

   ```R
   input_features <- tf$keras$Input(shape=dim(X_tf)[2])
   ```

   - **But** : Créer une couche d'entrée pour notre modèle, qui recevra les caractéristiques (features) des nœuds du graphe.
   - **Explication :**
     - `tf$keras$Input(...)` crée un tenseur d'entrée pour le modèle.
     - `shape=dim(X_tf)[2]` spécifie la dimension des caractéristiques d'entrée.
       - `X_tf` est un tenseur TensorFlow contenant les caractéristiques des nœuds.
       - `dim(X_tf)[2]` correspond au nombre de caractéristiques par nœud.
   - **Analogie** : Pensez à la couche d'entrée comme à la porte d'entrée de notre réseau de neurones, où chaque nœud apporte ses informations initiales.

**Première couche de convolution sur graphe :**

   ```R
   output <- spektral$layers$GCNConv(16L, activation='relu')$call(list(input_features, A_tf))
   ```

   - **But** : Ajouter une couche qui transformera les caractéristiques des nœuds en utilisant les informations de leurs voisins directs dans le graphe.
   - **Explication :**
     - `spektral$layers$GCNConv(16L, activation='relu')` crée une couche de convolution sur graphe avec 16 unités de sortie (neurones) et la fonction d'activation ReLU.
       - **GCNConv** : Une couche qui applique une opération de convolution sur les graphes, permettant à chaque nœud de combiner ses caractéristiques avec celles de ses voisins.
     - `...$call(list(input_features, A_tf))` applique la couche aux données d'entrée.
       - **Arguments :**
         - `input_features` : Les caractéristiques initiales des nœuds.
         - `A_tf` : La matrice d'adjacence du graphe (représente les connexions entre les nœuds).
   - **Résultat** : On obtient de nouvelles caractéristiques pour chaque nœud, enrichies par les informations de leurs voisins.

**Deuxième couche de convolution sur graphe :**

   ```R
   output <- spektral$layers$GCNConv(16L, activation='relu')$call(list(output, A_tf))
   ```

   - **But** : Affiner davantage les caractéristiques des nœuds en considérant les voisins des voisins.
   - **Explication :**
     - Cette couche prend en entrée les caractéristiques déjà transformées par la première couche (`output`).
     - En appliquant une deuxième couche, le modèle peut capturer des relations plus complexes et des informations provenant de nœuds plus éloignés dans le graphe.
   - **Pourquoi plusieurs couches ?**
     - La première couche agrège les informations des voisins immédiats.
     - La deuxième couche permet d'atteindre les voisins des voisins, capturant ainsi une structure plus globale du graphe.

**Définition du modèle final :**

   ```R
   model <- tf$keras$Model(inputs=input_features, outputs=output)
   ```

   - **But** : Créer un modèle de réseau de neurones complet en spécifiant les entrées et les sorties.
   - **Explication :**
     - `tf$keras$Model(...)` crée un objet modèle qui regroupe les couches définies.
     - `inputs=input_features` indique que les caractéristiques initiales des nœuds sont l'entrée du modèle.
     - `outputs=output` spécifie que la sortie du modèle est le résultat de la dernière couche (les nouvelles caractéristiques des nœuds).
   - **Analogie** : C'est comme construire une machine où l'on sait ce qui entre (les données brutes) et ce qui sort (les données transformées), en passant par plusieurs étapes de transformation.

**Concepts clés pour les débutants :**

- **Fonction d'Activation (`relu`) :**
  - Introduit de la non-linéarité dans le modèle, ce qui permet de modéliser des relations complexes.
  - **ReLU (Rectified Linear Unit)** : Défini comme `f(x) = max(0, x)`, il transforme les valeurs négatives en zéro et laisse les positives inchangées.
  - **But** : Empêcher certains neurones de s'activer (valeur zéro) pour éviter que le modèle ne devienne trop complexe ou ne surapprenne les données.

**Exemple concret :**

- **Imaginons un réseau social :**
  - Les nœuds représentent des personnes.
  - Les liens représentent des amitiés.
  - Chaque personne a des caractéristiques (âge, profession, centres d'intérêt).
- **But du GCN :**
  - Prédire la probabilité qu'une personne soit intéressée par un certain produit ou événement.
  - En considérant non seulement ses propres caractéristiques, mais aussi celles de ses amis et des amis de ses amis.

**Résumé des étapes :**

1. **Définir l'entrée du modèle** : Les caractéristiques initiales des nœuds.
2. **Appliquer des couches de convolution sur graphe** : Pour agrandir les caractéristiques en incorporant les informations du graphe.
3. **Construire le modèle final** : En spécifiant les entrées et les sorties.
4. **Entraîner le modèle** : Avec des données étiquetées (si disponibles) pour apprendre à effectuer une tâche spécifique (par exemple, classification de nœuds).

**Points importants pour les débutants :**

- **Deep Learning sur Graphes** : Contrairement aux données tabulaires ou aux images, les graphes ont une structure complexe qui nécessite des méthodes adaptées.
- **Les GCN sont une extension des réseaux de neurones traditionnels** : Ils permettent de traiter des données structurées en graphe en adaptant les opérations de convolution.
- **Apprentissage des Représentations (Embeddings)** : Le modèle apprend à représenter chaque nœud par un vecteur (une liste de nombres) qui capture sa position et son rôle dans le graphe.

**En conclusion :**

- Les Graph Convolutional Networks sont une puissante méthode pour analyser des graphes en profondeur.
- En comprenant chaque étape de la construction du modèle, même sans expérience préalable en deep learning, on peut saisir comment les informations du graphe et des nœuds sont combinées pour produire des résultats significatifs.

N'hésitez pas à poser des questions ou à demander des éclaircissements sur des parties spécifiques si nécessaire !

### b. GAT

```R
# Charger les bibliothèques nécessaires
library(reticulate)
library(ggplot2)
library(Rtsne)

# Installer les paquets Python requis
py_install(c("tensorflow", "spektral", "numpy", "networkx", "pandas"), pip=TRUE)

# Lire les données depuis les fichiers CSV
nodes <- read.csv("nodes.csv", stringsAsFactors=FALSE)
links <- read.csv("links.csv", stringsAsFactors=FALSE)

# Importer les modules Python nécessaires
tf <- import("tensorflow")
np <- import("numpy")
spektral <- import("spektral")
nx <- import("networkx")
pd <- import("pandas")

# Convertir les dataframes R en dataframes pandas
py_nodes <- r_to_py(nodes)
py_links <- r_to_py(links)

# S'assurer que les identifiants sont des entiers
py_links$source <- py_links$source$astype("int")
py_links$target <- py_links$target$astype("int")

# Construire le graphe en Python avec NetworkX
G <- nx$from_pandas_edgelist(py_links, source='source', target='target', edge_attr='weight', create_using=nx$Graph())

# Générer la matrice d'adjacence
A <- nx$adjacency_matrix(G)
A <- A$toarray()

# Préparer les caractéristiques des nœuds (features)
typeacteur_dummies <- pd$get_dummies(py_nodes$typeacteur)
opinionpolitique_dummies <- pd$get_dummies(py_nodes$opinionpolitique)
features_df <- pd$concat(list(typeacteur_dummies, opinionpolitique_dummies), axis=1)
features <- features_df$values

# Convertir les caractéristiques et la matrice d'adjacence en tenseurs TensorFlow
X_tf <- tf$convert_to_tensor(features, dtype=tf$float32)
A_tf <- tf$convert_to_tensor(A, dtype=tf$float32)

# Préparer les étiquettes en utilisant 'opinionpolitique'
labels <- as.factor(nodes$opinionpolitique)
labels_numeric <- as.numeric(labels) - 1  # Les labels commencent à 0
num_classes <- length(unique(labels_numeric))
labels_onehot <- tf$one_hot(labels_numeric, num_classes)

# Construire le modèle GAT avec Spektral
inputs <- tf$keras$Input(shape=ncol(features))
gat_layer <- spektral$layers$GATConv(8L, activation='elu', attn_heads=8L, concat_heads=TRUE)$call(list(inputs, A_tf))
output_layer <- spektral$layers$GATConv(num_classes, activation='softmax', attn_heads=1L, concat_heads=FALSE)$call(list(gat_layer, A_tf))
model <- tf$keras$Model(inputs=inputs, outputs=output_layer)

# Compiler le modèle
model$compile(optimizer='adam', loss='categorical_crossentropy', metrics='accuracy')

# Entraîner le modèle
model$fit(X_tf, labels_onehot, epochs=100L, batch_size=nrow(nodes), verbose=0L)

# Extraire les embeddings du modèle (avant la couche de sortie)
embedding_model <- tf$keras$Model(inputs=inputs, outputs=gat_layer)
embeddings <- embedding_model$predict(X_tf)

# Convertir les embeddings en data frame R
embeddings_df <- as.data.frame(embeddings)
embeddings_df$node_id <- nodes$id

# Réaliser une réduction de dimension avec t-SNE
tsne_results <- Rtsne(embeddings_df[, 1:ncol(embeddings)-1], dims=2, perplexity=5, verbose=FALSE, max_iter=500)

embeddings_df$tsne_x <- tsne_results$Y[,1]
embeddings_df$tsne_y <- tsne_results$Y[,2]

# Fusionner les embeddings avec les données de nœuds
nodes_embeddings <- merge(nodes, embeddings_df[, c('node_id', 'tsne_x', 'tsne_y')], by.x='id', by.y='node_id', all.x=TRUE)

# Visualiser les embeddings avec ggplot2
ggplot(nodes_embeddings, aes(x=tsne_x, y=tsne_y, color=typeacteur, shape=opinionpolitique)) +
  geom_point(size=3) +
  theme_minimal() +
  labs(title="Visualisation t-SNE des embeddings GAT")
```

**Explication détaillée du code pour les étudiants en sciences sociales computationnelles**

Dans ce bloc de code, nous mettons en œuvre un **Graph Attention Network (GAT)** en utilisant la bibliothèque **Spektral** pour la classification de nœuds dans un graphe. L'objectif est de prédire l'**opinion politique** des sites web (nœuds) en utilisant leurs caractéristiques et la structure du graphe. Voici une explication pas à pas du code, accompagnée d'exemples de sorties à chaque étape.

**Préparer les caractéristiques des nœuds (features)**

```R
typeacteur_dummies <- pd$get_dummies(py_nodes$typeacteur)
opinionpolitique_dummies <- pd$get_dummies(py_nodes$opinionpolitique)
features_df <- pd$concat(list(typeacteur_dummies, opinionpolitique_dummies), axis=1)
features <- features_df$values
```

**Explication :**

- **Encodage One-Hot des variables catégorielles :** Les attributs catégoriels `typeacteur` et `opinionpolitique` sont convertis en variables binaires à l'aide de la fonction `get_dummies` de pandas. Cela transforme chaque catégorie en une colonne distincte avec des valeurs 0 ou 1.

**Exemple de sortie :**

Supposons que nous ayons les données suivantes pour trois nœuds :

| id | typeacteur   | opinionpolitique |
|----|--------------|------------------|
| 1  | gouvernement | gauche           |
| 2  | média        | droite           |
| 3  | ONG          | centre           |

Après encodage :

**typeacteur_dummies :**

| gouvernement | média | ONG |
|--------------|-------|-----|
| 1            | 0     | 0   |
| 0            | 1     | 0   |
| 0            | 0     | 1   |

**opinionpolitique_dummies :**

| gauche | droite | centre |
|--------|--------|--------|
| 1      | 0      | 0      |
| 0      | 1      | 0      |
| 0      | 0      | 1      |

**features_df (concaténation des deux) :**

| gouvernement | média | ONG | gauche | droite | centre |
|--------------|-------|-----|--------|--------|--------|
| 1            | 0     | 0   | 1      | 0      | 0      |
| 0            | 1     | 0   | 0      | 1      | 0      |
| 0            | 0     | 1   | 0      | 0      | 1      |

**Interprétation :**

Chaque nœud est représenté par un vecteur binaire combinant son type d'acteur et son opinion politique.

**Conversion des caractéristiques et de la matrice d'adjacence en tenseurs TensorFlow**

```R
X_tf <- tf$convert_to_tensor(features, dtype=tf$float32)
A_tf <- tf$convert_to_tensor(A, dtype=tf$float32)
```

**Explication :**

- **X_tf :** Tenseur contenant les caractéristiques des nœuds, prêt pour être utilisé comme entrée dans le modèle TensorFlow.
- **A_tf :** Tenseur représentant la matrice d'adjacence du graphe, nécessaire pour les opérations de convolution sur graphes.

**Exemple de sortie :**

Si `features` est une matrice de dimensions (3, 6), alors `X_tf` sera un tenseur de forme (3, 6). De même, si `A` est une matrice (3, 3), `A_tf` sera un tenseur de forme (3, 3).

**Préparer les étiquettes en utilisant 'opinionpolitique'**

```R
labels <- as.factor(nodes$opinionpolitique)
labels_numeric <- as.numeric(labels) - 1  # Les labels commencent à 0
num_classes <- length(unique(labels_numeric))
labels_onehot <- tf$one_hot(labels_numeric, num_classes)
```

**Explication :**

- **Conversion en facteurs :** Transforme la colonne `opinionpolitique` en un type factoriel pour faciliter l'encodage.
- **Conversion en numériques :** Les facteurs sont convertis en nombres entiers (par exemple, gauche=1, droite=2, centre=3) et ajustés pour commencer à 0.
- **Nombre de classes :** Calcule le nombre total de classes (opinions politiques uniques).
- **Encodage One-Hot des labels :** Transforme les labels numériques en vecteurs binaires pour l'apprentissage supervisé.

**Exemple de sortie :**

Avec les labels numériques :

| id | labels_numeric |
|----|----------------|
| 1  | 0              | (gauche)
| 2  | 1              | (droite)
| 3  | 2              | (centre)

**labels_onehot :**

| classe_gauche | classe_droite | classe_centre |
|---------------|---------------|---------------|
| 1             | 0             | 0             |
| 0             | 1             | 0             |
| 0             | 0             | 1             |

---

**Construire le modèle GAT avec Spektral**

```R
inputs <- tf$keras$Input(shape=ncol(features))
gat_layer <- spektral$layers$GATConv(8L, activation='elu', attn_heads=8L, concat_heads=TRUE)$call(list(inputs, A_tf))
output_layer <- spektral$layers$GATConv(num_classes, activation='softmax', attn_heads=1L, concat_heads=FALSE)$call(list(gat_layer, A_tf))
model <- tf$keras$Model(inputs=inputs, outputs=output_layer)
```

**Explication :**

- **Définition de l'entrée :** Le modèle prend en entrée les caractéristiques des nœuds.
- **Première couche GAT :**
  - **8 unités de sortie**, fonction d'activation 'elu'.
  - **8 têtes d'attention (attn_heads=8L)**, ce qui permet au modèle de capturer différentes relations d'attention entre les nœuds.
  - **concat_heads=TRUE** : Les sorties des têtes d'attention sont concaténées, augmentant la richesse des représentations.
- **Seconde couche GAT :**
  - **Nombre d'unités égal au nombre de classes**, activation 'softmax' pour la classification.
  - **1 tête d'attention**, car nous n'avons besoin que d'une estimation finale des probabilités de classe.
  - **concat_heads=FALSE** : Les sorties ne sont pas concaténées.
- **Construction du modèle :** Combine les couches pour créer le modèle final.

**Interprétation :**

Le modèle GAT apprend à pondérer l'importance des voisins de chaque nœud en fonction des données, ce qui est particulièrement utile pour capturer des relations complexes dans le graphe.

**Compiler le modèle**

```R
model$compile(optimizer='adam', loss='categorical_crossentropy', metrics='accuracy')
```

**Explication :**

- **Optimiseur 'adam' :** Un algorithme d'optimisation adaptatif efficace pour l'apprentissage profond.
- **Loss 'categorical_crossentropy' :** Fonction de perte appropriée pour la classification multi-classes.
- **Metrics 'accuracy' :** Pour évaluer la performance du modèle pendant l'entraînement

**Entraîner le modèle**

```R
model$fit(X_tf, labels_onehot, epochs=100L, batch_size=nrow(nodes), verbose=0L)
```

**Explication :**

- **X_tf :** Les caractéristiques des nœuds en entrée.
- **labels_onehot :** Les labels encodés en One-Hot en sortie.
- **epochs=100L :** Le modèle va passer 100 fois sur l'ensemble des données.
- **batch_size=nrow(nodes) :** Utilisation de la totalité des données à chaque itération (apprentissage par batch complet).
- **verbose=0L :** Pas d'affichage de l'avancement pendant l'entraînement.

**Exemple de sortie :**

L'entraînement produit un modèle capable de prédire l'opinion politique des nœuds avec une certaine précision. Bien que nous n'ayons pas affiché les métriques pendant l'entraînement, nous pouvons les évaluer par la suite.

**Extraire les embeddings du modèle (avant la couche de sortie)**

```R
embedding_model <- tf$keras$Model(inputs=inputs, outputs=gat_layer)
embeddings <- embedding_model$predict(X_tf)
```

**Explication :**

- **Création d'un modèle pour les embeddings :** Nous définissons un nouveau modèle qui a les mêmes entrées mais dont la sortie est la couche cachée `gat_layer`.
- **Prédiction des embeddings :** En passant `X_tf` à ce modèle, nous obtenons les embeddings pour chaque nœud.

**Interprétation :**

Les **embeddings** sont des vecteurs de dimension réduite qui capturent les informations structurales et attributives des nœuds. Ils peuvent être utilisés pour diverses tâches comme la visualisation, le clustering ou la détection d'anomalies.

**Exemple de sortie :**

Si `gat_layer` produit des vecteurs de dimension 64 (8 unités x 8 têtes d'attention), alors `embeddings` sera une matrice de dimensions (nombre de nœuds, 64).


**Applications potentielles :**

- **Analyse des réseaux sociaux :** Comprendre les dynamiques d'influence et les relations entre différents acteurs.
- **Détection de communautés :** Identifier des groupes d'acteurs similaires ou des communautés au sein du réseau.
- **Recommandation personnalisée :** Utiliser les embeddings pour recommander des contenus ou des connexions pertinentes.

En maîtrisant ces techniques, vous serez en mesure d'appliquer des modèles avancés d'apprentissage profond aux graphes, ouvrant la voie à de nouvelles perspectives en sciences sociales computationnelles.