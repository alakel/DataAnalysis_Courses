En sociologie des réseaux, la notion de **rôle** représente les comportements et relations spécifiques associés aux positions des acteurs au sein d’une structure sociale. Cette idée trouve son origine dans les travaux de chercheurs comme Georg Simmel, qui s’intéressait aux formes de relations entre individus, et elle s’est développée davantage avec l’analyse des réseaux sociaux. Un rôle, dans ce contexte, est défini par les relations d’un acteur avec d’autres acteurs plutôt que par ses caractéristiques individuelles.

Le blockmodeling est une méthode puissante pour analyser les structures sociales complexes en réseaux, particulièrement en sciences sociales où l’on cherche à identifier les **rôles sociaux** et **positions structurelles** sans se limiter à des catégories prédéfinies. Contrairement aux méthodes traditionnelles basées sur des attributs ou des catégories fixes, le blockmodeling vise à révéler la **structure sous-jacente d’un réseau** en regroupant les acteurs selon leur **équivalence structurelle** — c’est-à-dire, la similarité de leurs patterns de relations avec les autres membres du réseau. 

Cette approche est particulièrement utile pour l’analyse des **réseaux multiples**, où les liens entre individus peuvent varier en nature (ex. amitié, relations professionnelles, affiliations politiques). Ce cours présente les fondements théoriques du blockmodeling, ses applications méthodologiques, et les algorithmes principaux nécessaires à sa mise en œuvre.
### 1. Méthodes de Blockmodeling
#### 1.1. Fondements Théoriques du Blockmodeling

**Motivation et Contexte**

Le blockmodeling a été développé pour répondre à une limitation des méthodes sociométriques traditionnelles. Dans les années 1970, **White, Boorman et Breiger** ont introduit cette approche pour identifier des **positions sociales** et **rôles** dans des réseaux sociaux multiples, sans imposer de catégories fixes. Leur hypothèse fondamentale est que les rôles sociaux peuvent être modélisés par des **blocs structurellement équivalents**. En d’autres termes, ils proposent de regrouper les individus en blocs si leurs patterns de relations sont similaires.

**Exemple de motivation** : Un individu dans un réseau social peut jouer des rôles multiples (ami, collègue, partenaire de sport) selon les relations spécifiques qu’il entretient. Le blockmodeling permet d’identifier ces rôles en analysant les liens d’un individu avec d’autres, plutôt qu’en se basant sur ses caractéristiques personnelles (âge, statut social, etc.).

**Concepts Clés : Équivalence Structurelle et Zeroblocks**

Le blockmodeling repose sur deux concepts principaux :

1. **Équivalence Structurelle** : Deux individus sont structurellement équivalents s’ils entretiennent des relations similaires avec d’autres individus dans le réseau. Mathématiquement, on considère deux acteurs, \(i\) et \(j\), structurellement équivalents si, pour tout autre acteur \(k\), les relations de \(i\) avec \(k\) sont identiques à celles de \(j\) avec \(k\).

2. **Zeroblocks** : Un zeroblock est un bloc où aucun lien n'existe entre les membres de deux groupes. Par exemple, dans un réseau professionnel, les membres de différents services peuvent être regroupés en zeroblocks si les interactions entre eux sont inexistantes. Ces zeroblocks mettent en évidence des **barrières sociales** ou des **frontières de rôle**.

Ces deux concepts permettent d’identifier des patterns relationnels sans imposer des liens de type « clique » ou « groupe » rigides, offrant ainsi une vision plus flexible de la structure sociale.
#### 1. 2. Méthodologie du Blockmodeling : Modélisation et Calculs

La méthodologie du blockmodeling repose sur la création de **matrices de relations**, la **partition en blocs**, et l’**analyse des relations entre blocs**. Nous allons examiner chaque étape méthodologique.

**Construction des Matrices d’Adjacence**

Pour chaque type de relation dans un réseau, on crée une **matrice d'adjacence** \(A\) où \(a_{ij} = 1\) indique qu’il existe une relation entre l’acteur \(i\) et \(j\), et \(a_{ij} = 0\) sinon. Cela permet de représenter graphiquement les relations sociales sous forme de matrices, facilitant le traitement par algorithmes.

**Exemple de matrice d’adjacence** :
Pour une relation d’amitié dans un réseau de quatre individus, la matrice pourrait être la suivante :

$$

A = \begin{pmatrix}
0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 \\
0 & 1 & 0 & 1 \\
1 & 0 & 1 & 0 \\
\end{pmatrix}

$$

Chaque ligne et colonne représente un acteur et les 1 indiquent des liens d’amitié. Ces matrices sont essentielles pour identifier les blocs.

**Partitionnement : Algorithme de CONCOR et Méthodes Stochastiques**

**Algorithme CONCOR** 
L'algorithme CONCOR (**Convergence of Iterated CORrelations**) est un algorithme itératif qui calcule les corrélations entre les lignes (ou colonnes) des matrices d’adjacence. Il procède par étapes :

1. **Initialisation** : On calcule la première matrice de corrélation.
2. **Itérations** : On continue de calculer les corrélations jusqu’à ce que les valeurs convergent.
3. **Bipartition** : Lorsque les valeurs convergent, les acteurs sont divisés en deux groupes selon le signe de leur corrélation, ce qui donne des blocs structurellement équivalents.

**Blockmodeling Stochastique et Algorithmes Bayésiens**  
Dans les réseaux modernes, plus grands et plus complexes, on utilise des **blockmodels stochastiques** pour prendre en compte les variations aléatoires dans les relations. **Snijders et Nowicki (1997)** ont proposé un modèle stochastique où chaque relation est considérée comme une **probabilité conditionnelle** de liens entre blocs.

Les algorithmes utilisés pour estimer ces probabilités incluent :
- **Algorithme EM** (Expectation-Maximization), pour maximiser la vraisemblance des blocs latents.
- **Échantillonnage de Gibbs** : méthode bayésienne qui utilise des itérations pour évaluer les probabilités d'appartenance à un bloc, très utile pour les grands réseaux.

**Identification des Zeroblocks et Construction de l’Image Binaire**

Une fois les blocs identifiés, on peut construire une **image binaire du réseau**, où chaque bloc est représenté par un 1 (s’il existe des liens) ou un 0 (si le bloc est un zeroblock). Cette image binaire simplifie la visualisation des relations entre groupes, en révélant les **barrières structurelles** au sein du réseau.

**Exemple d’image binaire** :
Supposons que nous avons trois blocs dans un réseau social :
$$
\text{image}(I, J) = 
\begin{cases}
1 & \text{si le bloc (I, J) n'est pas un zeroblock} \\
0 & \text{si le bloc (I, J) est un zeroblock}
\end{cases}
$$

## 2 Application en R : Identification des Rôles avec l’Équivalence Structurale et le Blockmodeling**

Dans cette partie, nous allons explorer diverses méthodes de **blockmodeling** pour identifier les rôles et les positions dans les réseaux sociaux. Ces techniques permettent de regrouper les nœuds ayant des relations structurellement similaires avec d’autres nœuds, un concept central en sociologie des réseaux pour analyser les **équivalences structurelles** et les **blocs régularisés**.

Nous aborderons ici les principales méthodes de blockmodeling disponibles en R, en utilisant les packages `igraph` et `blockmodeling`, ainsi que certaines approches pour les réseaux bipartites ou multi-couches.
### 2.1. **Équivalence Structurale : Similitude de Jaccard**

L'équivalence structurale regroupe les nœuds ayant des **patterns de connexions similaires** avec les autres nœuds, c’est-à-dire ceux partageant les mêmes voisins. Une façon de calculer cette équivalence est de passer par la **similarité de Jaccard**, qui évalue le ratio des voisins communs.

```R
# Calcul de la matrice de similarité de Jaccard
similarity_matrix <- similarity(net, method = "jaccard")

# Visualisation de la matrice de similarité
print(similarity_matrix)
```

Cette matrice de similarité représente la proximité structurelle des nœuds dans le réseau. 

Le clustering hiérarchique est appliqué pour regrouper les nœuds ayant des similarités de connexions fortes. Il aide à **partitionner les nœuds en blocs** ayant des relations similaires avec d’autres blocs.

```R
# Création de la matrice de dissimilarité (1 - similarité) pour le clustering
dist_matrix <- as.dist(1 - similarity_matrix)

# Clustering hiérarchique sur la matrice de dissimilarité
hc <- hclust(dist_matrix, method = "average")

# Partition en un nombre de blocs défini
k <- 3  # Par exemple, on choisit 3 blocs
clusters <- cutree(hc, k = k)

# Assignation des blocs aux nœuds et visualisation
V(net)$block <- clusters
plot(net, vertex.color = V(net)$block, vertex.label = V(net)$name, main = "Blockmodeling par Clustering Hiérarchique")
```

### 2.2. **Blockmodeling Stochastique**

Le **blockmodeling stochastique** propose une approche probabiliste pour détecter des blocs de nœuds, en cherchant la meilleure partition selon un critère de vraisemblance. Cette méthode est particulièrement utile pour les grands réseaux où les connexions ne sont pas strictement déterministes.

Pour cela, nous utilisons le package `blockmodeling` avec des algorithmes d’optimisation pour déterminer les partitions de blocs.

```R
library(blockmodeling)

# Conversion du réseau en matrice d'adjacence pour le blockmodeling stochastique
adj_matrix <- as_adjacency_matrix(net, sparse = FALSE)

# Application de l'algorithme de partitionnement stochastique
res <- optRandomParC(adj_matrix, k = k)  # ici, k est le nombre de blocs

# Affichage des blocs obtenus
print(res$cluster)
```

Cette approche utilise des itérations aléatoires pour maximiser la probabilité des blocs et est efficace dans les réseaux denses ou bruités.

**Blockmodeling pour Réseaux Signés**

Certains réseaux contiennent des **liens signés** (positifs et négatifs), nécessitant une méthode de partition spécifique. Le package `blockmodeling` offre des fonctions dédiées pour les réseaux signés, permettant de partitionner les nœuds tout en tenant compte de la polarité des relations.

```R
# Application de blockmodeling pour réseaux signés
res_signed <- optRandomSignedParC(adj_matrix, k = k)  # spécifiquement pour réseaux signés

# Affichage des clusters dans les réseaux signés
print(res_signed$cluster)
```

Cette méthode est utile pour des contextes tels que les réseaux d’opinion ou de conflit, où les relations peuvent être à la fois positives et négatives.

**Blockmodeling Régularisé**

Le **blockmodeling régularisé** introduit des pénalités dans le modèle pour éviter le surapprentissage, en particulier dans les grands réseaux. Cela est essentiel pour gérer la complexité des modèles et garantir que les blocs identifiés restent interprétables.

```R
# Application de blockmodeling régularisé
res_regularized <- optRegularizedParC(adj_matrix, k = k)

# Affichage des résultats régularisés
print(res_regularized$cluster)
```

La régularisation ajoute un contrôle supplémentaire en limitant la complexité des blocs, permettant une analyse plus robuste et généralisable.
### 2.3. Comparaison et Interprétation des Méthodes de Blockmodeling

**Comparaison des Méthodes**

- **Équivalence structurale et clustering hiérarchique** : Ces méthodes sont adaptées aux petits réseaux et permettent de regrouper les nœuds ayant des connexions identiques, idéales pour identifier des rôles strictement similaires.
  
- **Blockmodeling stochastique** : Avec son approche probabiliste, cette méthode est plus flexible pour les grands réseaux ou lorsque les relations sont bruitées, car elle ne nécessite pas de similarité exacte.

- **Blockmodeling régularisé** : Cette méthode est importante pour les réseaux denses et de grande taille, car elle introduit une pénalité pour éviter le surajustement, assurant ainsi des blocs stables.

- **Blockmodeling pour réseaux signés** : Crucial pour les réseaux où les relations peuvent être positives ou négatives, cette méthode permet d’identifier des blocs dans des contextes de conflit ou de coopération.

## 3. Cas d’Application en Sciences Sociales

Applications et Cas Pratiques du Blockmodeling

Les applications pratiques du blockmodeling sont vastes et couvrent des domaines comme la sociologie, la criminologie, et l’analyse organisationnelle. Voici quelques exemples d'utilisation.

##### 3.1 Analyse des Rôles dans les Organisations

Dans le cadre de l'analyse des rôles au sein des organisations, le blockmodeling est un outil puissant pour décrypter les structures cachées d'interactions entre les employés et les départements. Au-delà de simples organigrammes formels, il permet d'identifier les **rôles organisationnels effectifs** tels que les **superviseurs**, les **collaborateurs** actifs et les **services isolés**. En intégrant des données de communication (emails, réunions, collaborations sur des projets), le blockmodeling révèle comment se forment et évoluent les réseaux de travail au quotidien.

Prenons un cas classique d'application dans une grande entreprise où les départements – comme le marketing, les ressources humaines et la R&D – sont censés collaborer étroitement pour réaliser des projets transversaux. Un bloc central, par exemple, peut être composé d'un **superviseur** et de plusieurs **collaborateurs** directs qui échangent fréquemment des informations et coordonnent leurs actions. En utilisant le blockmodeling, on peut distinguer ce groupe comme un bloc de haute densité, montrant une **forte cohésion interne**. Ce groupe central peut aussi interagir sporadiquement avec d'autres blocs dans l'organisation, signalant les occasions de collaboration transversale.

D'un autre côté, il est courant de voir émerger des **zeroblocks**, c’est-à-dire des blocs sans liens entre eux. Dans une étude menée par Cross et Parker (2004), le blockmodeling a permis de découvrir que les employés du service des finances étaient souvent isolés des autres départements. Ce manque de communication avec les autres services a été interprété comme un **symptôme d'isolement fonctionnel**, où des employés se retrouvent déconnectés du flux global de l'information, ce qui peut nuire à leur contribution aux projets interdisciplinaires. En visualisant les données de communication par blockmodeling, les chercheurs ont démontré comment ces **services isolés** échappaient aux processus de coordination informels qui contribuent à l'innovation et à l'efficacité organisationnelle.

**Étude de Cas : Rôles des Superviseurs et Collaborateurs dans une Organisation Complexe**

Une recherche conduite par Burt (1992) s'intéressait aux **superviseurs**, identifiables par leur rôle de relais dans les échanges entre différents groupes de collaborateurs. Le blockmodeling a permis de dégager des "ponts structurels" entre équipes : par exemple, des managers de projet jouant un rôle de médiateurs entre les départements de R&D et de production. Ce rôle a été identifié par leur appartenance à plusieurs blocs avec des liens inter-blocs fréquents, illustrant leur fonction de **coordination entre différentes unités**. En effet, ce type de nœuds agissant comme « liens faibles » (au sens de Granovetter) entre des sous-groupes favorise la diffusion rapide de l’information et la collaboration en dehors des silos.

Ces découvertes ont eu des implications directes pour les entreprises, notamment en matière de **formation et d'allocation des ressources**. Dans le cas de Burt, les superviseurs identifiés comme liens cruciaux ont été encouragés à renforcer leurs compétences en communication pour soutenir davantage leur rôle de médiateurs.

**Identification des Clusters et des Services Isolés**

Dans une autre étude, Snijders et ses collègues (1997) se sont penchés sur des organisations en réseau, où des **services isolés** pouvaient émerger en raison d’une division géographique ou de la spécialisation fonctionnelle. Par le biais du blockmodeling, ils ont découvert que les employés affectés à des filiales régionales avaient peu d'interactions avec le siège, formant ainsi des clusters isolés identifiés comme des zeroblocks. Cette configuration est souvent symptomatique de la **décentralisation de l’information** et d'une faible intégration au sein de l'organisation globale. En réponse, les entreprises ont pu restructurer leurs politiques de communication pour **réduire cet isolement fonctionnel**, facilitant l'échange d’informations et renforçant la cohérence des pratiques entre les différentes unités.

Grâce au blockmodeling, les chercheurs en sciences sociales peuvent aller au-delà des simples hiérarchies visibles pour découvrir la **structure effective de l’organisation**. La reconnaissance des rôles réels et la distinction des services isolés ou des superviseurs peuvent ainsi améliorer les politiques internes, renforcer la **cohésion organisationnelle** et favoriser la **transparence de l’information**. Ces approches offrent une nouvelle manière de visualiser et comprendre les dynamiques relationnelles, contribuant à une organisation plus efficiente et collaborative.

**Références :**
- Burt, R. S. (1992). *Structural Holes: The Social Structure of Competition*. Harvard University Press.
- Cross, R., & Parker, A. (2004). *The Hidden Power of Social Networks: Understanding How Work Really Gets Done in Organizations*. Harvard Business School Press.
- Snijders, T. A. B., & Nowicki, K. (1997). Estimation and Prediction for Stochastic Blockmodels for Graphs with Latent Block Structure. *Journal of Classification*, 14(1), 75-100.

##### 3.2 Étude des Réseaux Politiques et des Factions

Dans le domaine de la science politique, le blockmodeling offre des perspectives précieuses pour analyser les **réseaux politiques** et cartographier les **alliances** et **oppositions** entre groupes. Par exemple, les blocs peuvent identifier des **factions rivales** ou des groupes d’alliés, illustrant les dynamiques de soutien, de rivalité et d’influence entre différents acteurs. Ces informations permettent de visualiser non seulement les relations explicites entre les partis ou les individus, mais également les **connexions cachées** et les **divergences** idéologiques qui structurent le paysage politique.

**Analyse des Factions au sein du Congrès Américain**

Dans une recherche influente, Lorrain et White (1971) ont appliqué le blockmodeling pour étudier les alliances et factions au sein du Congrès américain. En analysant les **relations de vote** entre les membres, ils ont identifié plusieurs blocs de législateurs partageant des tendances de vote similaires. Certains blocs représentaient des partis politiques classiques, comme les démocrates et les républicains, mais d’autres ont révélé des **factions internes** : par exemple, une coalition de législateurs modérés prêts à voter avec l’opposition sur certains sujets. Ces blocs, non évidents à partir d’une simple analyse de vote, mettaient en lumière des **groupes de soutien mutuel** au sein même des partis, illustrant des alliances informelles et parfois transpartisanes.

Dans le cadre de cette analyse, certains blocs se sont également distingués comme **zeroblocks** — des blocs où les liens de soutien ou de vote étaient pratiquement absents. Cela a révélé des **clivages internes** au sein des partis, notamment entre les ailes progressistes et modérées chez les démocrates, et entre conservateurs modérés et ultra-conservateurs chez les républicains. Cette segmentation interne a permis de mieux comprendre les dynamiques politiques qui sous-tendent les **décisions législatives**, et les tensions qui entravent parfois l’unité de chaque parti.

**Bloc et Opposition : Alliances et Rivalités dans les Assemblées Locales**

Une autre application du blockmodeling s’est concentrée sur les conseils municipaux en France, où différents partis et factions cohabitent souvent. Les chercheurs, en s’appuyant sur le modèle de blockmodeling stochastique, ont pu distinguer des groupes d’alliés locaux et identifier des **factions opposées** qui, bien que cohabitant dans la même assemblée, s’opposaient systématiquement lors des votes. Par exemple, une étude menée par Lazega et Pattison (1999) a utilisé cette approche pour cartographier les **réseaux d’influence** dans plusieurs villes françaises, révélant comment certaines alliances dépassaient les frontières idéologiques pour se concentrer sur des enjeux locaux, comme le développement urbain ou les politiques environnementales.

Dans cette configuration, les blocs identifiés par le blockmodeling ont montré non seulement des alliances, mais aussi des **axes de conflits**, matérialisés par l’absence de liens entre certains blocs (zeroblocks), représentant ainsi des clivages fermes et des oppositions idéologiques marquées. Ces blocs permettaient de décrire les différentes coalitions au sein des assemblées locales et d’anticiper les alliances possibles ou improbables lors des prises de décision.

**Lutte pour l'Influence : Dynamique des Réseaux de Soutien en Campagne Électorale**

Le blockmodeling s’est également révélé utile pour analyser les réseaux de soutien lors des campagnes électorales. En étudiant les alliances formées par les candidats, les chercheurs ont pu identifier des blocs représentant des groupes de partisans et d'influenceurs locaux qui jouent un rôle clé dans le succès des candidats. Par exemple, les campagnes présidentielles américaines ont montré comment les candidats utilisent leurs alliances avec des politiciens locaux, des influenceurs et des groupes de soutien pour asseoir leur légitimité. Les blocs ainsi identifiés illustrent la capacité des candidats à mobiliser des ressources humaines et politiques autour de leur candidature.

Dans une étude comparative, Marsden et Friedkin (1994) ont appliqué le blockmodeling pour analyser ces réseaux de soutien, démontrant que certains blocs agissaient comme des relais stratégiques, transférant l'influence d'un candidat vers des groupes spécifiques de la population. Ces blocs servaient de médiateurs pour diffuser l’influence politique et atténuer les rivalités, permettant à certains candidats de contourner leurs opposants en s’appuyant sur des **alliés influents** situés à des points de passage stratégiques du réseau social.

Les applications du blockmodeling en science politique sont multiples et permettent de mieux saisir la **complexité des réseaux politiques** en détectant des structures cachées d’influence, d’alliance et de rivalité. Grâce à l’identification des blocs et zeroblocks, les chercheurs peuvent comprendre comment se forment les alliances, où résident les clivages les plus profonds, et comment les acteurs politiques utilisent leur position dans le réseau pour maximiser leur influence. Ces analyses ouvrent des perspectives pour des applications pratiques, telles que la **planification stratégique** des campagnes électorales, la gestion des **coalitions parlementaires**, et l’optimisation de l’**influence politique** dans les environnements de gouvernance locale et nationale.

**Références :**
- Lorrain, F., & White, H. C. (1971). Structural Equivalence of Individuals in Social Networks. *Journal of Mathematical Sociology*, 1(1), 49-80.
- Lazega, E., & Pattison, P. (1999). Multiplexity, generalized exchange and cooperation in organizations: A case study. *Social Networks*, 21(1), 67-90.
- Marsden, P. V., & Friedkin, N. E. (1994). Network studies of social influence. *Sociological Methods & Research*, 22(1), 127-151.

##### 3.3 Réseaux Criminels et Rôles Spécifiques

Le blockmodeling est particulièrement utile dans l'analyse des **réseaux criminels**, où il permet d'identifier des **sous-groupes spécialisés** au sein de l'organisation et de définir des rôles spécifiques tels que **leaders**, **exécuteurs**, et **facilitateurs**. Dans ces réseaux, chaque bloc ou segment relationnel identifié peut être interprété comme une unité fonctionnelle distincte, parfois autonome, mais toujours intégrée dans la hiérarchie du réseau criminel global.

**Cartographie des Rôles dans un Réseau Criminel**

Une étude influente menée par Morselli (2009) a appliqué le blockmodeling pour analyser les structures relationnelles au sein de réseaux criminels impliqués dans le trafic de drogue. En examinant les interactions au sein d'un cartel, l'étude a permis de distinguer plusieurs blocs jouant des rôles distincts dans l’organisation. Par exemple, les **leaders** ou chefs de cartel étaient au centre des relations et avaient des liens avec presque tous les autres blocs. Ils jouaient le rôle de décisionnaires stratégiques, supervisant l’ensemble des opérations.

D'autres blocs identifiés représentaient des groupes d'**exécuteurs**, chargés de tâches spécifiques telles que le transport ou la distribution des marchandises. Ces acteurs, bien qu'étant en contact avec les leaders, n’avaient que peu de liens entre eux, ce qui réduisait les risques en cas de démantèlement partiel du réseau. Enfin, un autre bloc était constitué de **facilitateurs**, des acteurs jouant un rôle de connexion avec des réseaux extérieurs, comme les blanchisseurs d’argent ou les intermédiaires financiers.

L'identification de ces blocs a permis non seulement de comprendre les fonctions au sein du réseau criminel, mais aussi de mieux cibler les actions des forces de l'ordre en identifiant les acteurs-clés qui, s’ils étaient neutralisés, pourraient perturber le fonctionnement de l’organisation.

**Les Zeroblocks : Identification des Segments Autonomes et Cloisonnés**

L'analyse des réseaux criminels montre souvent des **zeroblocks**, ou blocs sans liens avec d'autres groupes. Dans le contexte criminel, ces zeroblocks représentent souvent des segments autonomes de l’organisation, où les acteurs ne communiquent qu'avec un groupe limité de personnes pour minimiser les risques de divulgation en cas d’infiltration. Par exemple, dans une organisation hiérarchisée, les membres d’un zeroblock peuvent être constitués de **complices isolés** ou de groupes géographiquement distants, n’interagissant qu’avec un facilitateur unique. Ces configurations permettent au réseau de maintenir un haut niveau de **cloisonnement**, protégeant ainsi les informations sensibles et les identités des leaders.

**Application du Blockmodeling dans les Enquêtes Criminelles**

Le blockmodeling permet également aux enquêteurs de reconstruire des réseaux criminels fragmentés, notamment lorsqu’ils n'ont que des informations partielles sur les liens entre les membres. En analysant les interactions connues et en les comparant aux modèles de blockmodeling, les enquêteurs peuvent déduire les **structures de commandement** et les **routes logistiques** utilisées par le réseau.

Une application célèbre de cette approche a été réalisée par Sparrow (1991), qui a étudié les liens dans des organisations de trafic de stupéfiants. Son analyse a révélé que certains acteurs jouaient un rôle de “nœud central” dans la communication et la coordination, tandis que d’autres, plus en périphérie, étaient impliqués dans des tâches ponctuelles. Les acteurs centraux faisaient souvent partie d’un bloc stratégique, essentiel pour la coordination et la planification, tandis que les acteurs périphériques formaient des blocs isolés, intervenant dans des opérations spécifiques.

**Dynamique des Rôles et Réseaux Criminels : Limites et Perspectives**

Le blockmodeling offre une perspective puissante pour comprendre les **dynamiques internes** et les **rôles spécifiques** au sein des réseaux criminels, mais il est également limité par la nature partielle des données disponibles dans les enquêtes criminelles. Les chercheurs, en exploitant des méthodes bayésiennes de blockmodeling, tentent de pallier cette limite en estimant les liens probables entre acteurs basés sur des modèles stochastiques.

Dans une étude récente, Roberts et Everton (2011) ont appliqué des modèles de blockmodeling stochastiques pour analyser un réseau criminel international. Ils ont montré comment, même avec des données incomplètes, les modèles probabilistes pouvaient identifier les rôles fonctionnels des différents blocs, comme les cellules d’approvisionnement, les réseaux de distribution, et les connecteurs transfrontaliers.

L’utilisation du blockmodeling dans l’analyse des réseaux criminels offre des **outils de visualisation** et des **techniques d’inférence** pour démanteler des organisations complexes. En distinguant les rôles et en identifiant les blocs critiques et autonomes, le blockmodeling fournit aux forces de l’ordre et aux analystes des clés pour cibler les individus stratégiques dans les organisations criminelles. Cette approche structurelle aide non seulement à saisir les dynamiques internes d’un réseau, mais aussi à comprendre comment des configurations spécifiques de rôles et de relations protègent l'organisation de la détection et facilitent sa résilience face aux actions d'infiltration et de neutralisation.

**Références :**
- Morselli, C. (2009). *Inside Criminal Networks*. New York: Springer.
- Sparrow, M. K. (1991). The application of network analysis to criminal intelligence: An assessment of the prospects. *Social Networks*, 13(3), 251-274.
- Roberts, N., & Everton, S. F. (2011). *Strategies for Disrupting Dark Networks*. New York: Cambridge University Press.

# Conclusion

Le blockmodeling permet une compréhension avancée des structures sociales en réseaux en identifiant les **positions structurelles** et les **rôles sociaux** sans imposer de catégories a priori. À l’aide d’algorithmes tels que CONCOR et d’approches bayésiennes stochastiques, cette méthode capture des dynamiques complexes et révèle des segments de la société en réseaux difficiles à voir par d'autres approches.

Ce cours théorique sera suivi par une application pratique en R pour mettre en œuvre ces concepts à partir de données relationnelles. Vous apprendrez à :
- Créer des matrices d’adjacence en R
- Utiliser des fonctions pour identifier les blocs structurellement équivalents
- Appliquer des algorithmes d’estimation pour générer des blockmodels sur des données empiriques

En conclusion, le blockmodeling offre un cadre rigoureux et flexible pour l’analyse des réseaux sociaux, avec des applications théoriques et pratiques variées, des organisations aux groupes sociaux et aux réseaux d’influence.

