## Partie 1 : État de l'Art en Analyse des Triades et Phénomènes de Transitivité/Réciprocité

### 1.1. Contexte et Fondements Théoriques : Moreno et Heider

Les triades, formées de trois nœuds interconnectés, sont considérées comme les unités fondamentales pour étudier les configurations de réseaux sociaux. Les triades permettent ainsi de saisir des dynamiques telles que la **transitivité** (tendance des amis d’un ami à devenir également amis) et la **réciprocité** (tendance des liens à être réciproques dans les relations dirigées). Ces concepts sont essentiels pour comprendre la cohésion sociale, la formation de sous-groupes (clustering) et les processus de diffusion dans les réseaux.

L’analyse des triades en tant qu'unités de base pour comprendre les réseaux sociaux remonte à l’ère fondatrice de la sociométrie et des premières théories relationnelles. La sociométrie, introduite par **Jacob Moreno (1934)**, a jeté les bases de l’analyse formelle des relations interpersonnelles en utilisant des méthodes graphiques et mathématiques pour cartographier les liens sociaux. Le principal apport de Moreno réside dans l'idée que les relations triadiques ne sont pas de simples extensions de relations dyadiques (deux individus), mais qu'elles possèdent des propriétés uniques qui poussent la triade à rechercher une stabilisation. Dans une triade, la présence d'un troisième membre peut :

- **Renforcer** les liens existants entre deux individus, créant ainsi une cohésion de groupe plus forte.
- **Introduire des tensions** lorsque les préférences relationnelles sont asymétriques (par exemple, si un individu est rejeté par deux autres, il devient isolé dans le groupe).
- **Faciliter le rôle de médiation** : un individu dans une triade peut servir de médiateur entre deux autres, influençant leurs interactions de manière subtile.

La structure des triades a rapidement gagné en importance, car elle permet d’observer des motifs relationnels simples mais significatifs, qui illustrent les dynamiques d'affinité et d'exclusion. Moreno a utilisé ces concepts pour étudier des groupes divers, des classes scolaires aux prisons, et a démontré que les relations entre individus pouvaient être influencées par des facteurs invisibles mais puissants et systémique. 

**Fritz Heider (1946)** a poursuivi cette exploration des triades avec sa **théorie de la balance cognitive**, en introduisant un modèle théorique pour comprendre comment les relations évoluent vers des configurations stables. Heider postulait que les individus recherchent une cohérence cognitive dans leurs relations, ce qui les conduit à ajuster leurs attitudes pour atteindre un équilibre. Dans une triade, si deux individus entretiennent une relation positive (amitié ou accord) et chacun a un jugement similaire (positif ou négatif) sur une troisième personne, la structure devient "équilibrée". Cette balance cognitive se traduit ainsi par la tendance naturelle des individus à aligner leurs jugements en fonction de leurs relations existantes.

### 1.2. Théorie de l’Équilibre Structurel

**Cartwright et Harary (1956)** ont formalisé la théorie de Heider en introduisant la **théorie de l’équilibre structurel**. Cette théorie vise à comprendre les dynamiques de stabilité dans les configurations de relations entre individus, en se concentrant sur les triades comme unité d’analyse fondamentale. L’objectif de leur article est de définir rigoureusement le concept d’équilibre à l’aide de la théorie des graphes, afin de modéliser les interactions positives et négatives dans les réseaux sociaux.

L’article part du constat de Heider selon lequel les individus tendent à organiser cognitivement leurs relations de manière équilibrée. Une triade (ensemble de trois entités) est dite « équilibrée » si elle respecte certaines configurations stables, comme lorsque deux amis partagent un même ami ou ennemi. En revanche, une triade est déséquilibrée si elle inclut des relations contradictoires, créant des tensions cognitives. Cartwright et Harary soulignent toutefois les limitations de cette approche pour analyser des réseaux plus complexes, où les relations peuvent être asymétriques ou comporter plus de trois entités.

L’approche de Cartwright et Harary repose sur des concepts de base de la **théorie des graphes** :
- **Graphes signés** : ils introduisent des graphes où chaque lien entre deux entités peut être positif (relation d’amitié, d’alliance) ou négatif (antagonisme, rivalité).
- **Cycles** : dans un graphe, un cycle est un ensemble de liens fermés qui reviennent à leur point de départ. Un cycle est considéré comme équilibré si le produit des signes de ses liens est positif (par exemple, deux liens négatifs et un lien positif).
- **S-Graphes et S-Digraphes** : les auteurs utilisent les S-graphes (graphes signés) pour représenter les relations symétriques et les S-digraphes pour les relations asymétriques, comme dans le cas où un individu peut aimer une autre personne sans réciprocité
La théorie formelle développée par Cartwright et Harary stipule qu’un graphe est équilibré si **tous ses cycles sont positifs**. Ils démontrent que pour garantir l’équilibre d’un graphe contenant un nombre quelconque d’entités, il suffit de vérifier que tous les cycles formés par les nœuds sont positifs. Cela signifie que, dans un réseau équilibré, les individus s’organisent en deux sous-groupes, chacun marqué par des relations positives en son sein et des relations négatives avec l’autre groupe.

L’apport majeur de Cartwright et Harary réside dans leur formulation mathématique de la théorie de l’équilibre, qui rend possible son application à des systèmes sociaux complexes. Leur modèle formel de l’équilibre permet de caractériser des configurations sociales stables et de prédire comment les réseaux sociaux peuvent évoluer pour réduire les tensions. Ils introduisent également la notion de **degré d'équilibre**, permettant de mesurer le niveau de balance d’un graphe qui n’est pas complètement équilibré, ce qui offre un outil de mesure quantitatif pour des analyses empiriques. Enfin, ils suggèrent que cette théorie peut être appliquée à d’autres types de réseaux, tels que les réseaux de communication ou les systèmes de pouvoir, au-delà des simples configurations cognitives individuelles.
### 1.3 Typologie des Triades et Modèles d’Équilibre Structurel (structural balance)

Les triades dans les réseaux orientés peuvent être classées en 16 types différents, chacun représentant une configuration unique des relations entre trois nœuds. Les types de triades incluent des configurations **fermées** (où les trois nœuds sont reliés), **ouvertes** (où un nœud est isolé) et des configurations de déséquilibre structurel, où certaines relations sont négatives (dans les réseaux où les liens peuvent être conflictuels). Par exemple, dans les réseaux d’amitié, une triade fermée indique que les trois personnes sont mutuellement amies, ce qui tend à stabiliser les relations, tandis qu'une triade ouverte peut révéler une relation en formation ou en dissolution.

**Davis (1967)** a approfondi cette typologie en proposant des modèles probabilistes pour évaluer la stabilité des triades dans des réseaux où les relations peuvent être positives ou négatives. Ces modèles d’équilibre structurel permettent d’analyser la tendance des réseaux sociaux à évoluer vers des états d’équilibre en fonction de règles de similarité et d’attrait/répulsion. 

**Holland et Leinhardt (1977)** ont, pour leur part, proposé des modèles de transitivité et de réciprocité permettant de mesurer quantitativement la probabilité de formation des triades en fonction de la présence de liens dans un réseau.
### 1.4 Modélisation Statistique des Triades

La **transitivité** est une propriété essentielle des réseaux sociaux, souvent observée dans des contextes où les individus forment des groupes denses et interconnectés. Par exemple, si Alice est amie avec Bob, et Bob avec Charlie, il est probable qu'Alice et Charlie deviennent également amis, formant ainsi une triade fermée. La transitivité, souvent mesurée par le **coefficient de clustering**, décrit la densité des liens au sein des sous-groupes du réseau. Le **clustering** (ou groupement) est l’agrégation des triades fermées dans un réseau, signalant que les membres du groupe ont tendance à avoir des liens indirects par l’intermédiaire de leurs amis communs.

La **réciprocité** est une autre caractéristique fondamentale des réseaux dirigés, où un lien entre deux individus est souvent mutuel. Dans les réseaux sociaux humains, la réciprocité est observée comme un phénomène de base dans les relations d’échange, de soutien et d'interaction sociale. Des chercheurs comme **Wasserman et Faust (1994)** ont quantifié ce concept dans les réseaux, en analysant la probabilité qu’un lien dirigé d’un nœud vers un autre soit réciproque. Dans des contextes comme les réseaux de communication, de collaboration et d'échanges économiques, la réciprocité des triades joue un rôle central dans la cohésion et la robustesse des réseaux.
## Partie 2 : Mise en Application des Concepts Théoriques en R

### 2.1 Représentation des Triades dans les Graphes

**Extraction et Classification des Triades**

Pour analyser les triades dans un graphe, nous pouvons utiliser la fonction `triad_census()` du package **igraph**, qui compte les différentes configurations de triades selon la typologie des 16 types de Holland et Leinhardt (1977).

```R
# Calcul du recensement des triades
triad_counts <- triad_census(g)
names(triad_counts) <- c("003", "012", "102", "021D", "021U", "021C", "111D", "111U", "030T", "030C", "201", "120D", "120U", "120C", "210", "300")
print(triad_counts)
```

Chaque code de triade représente une configuration spécifique entre trois nœuds.

Voici la signification de chacune des triades et leur interprétation en analyse réseau, notamment en sciences sociales :

1. **“003” - Triade nulle**

• **Signification** : Aucun lien n’existe entre les trois nœuds. Les trois nœuds sont totalement isolés les uns des autres.

• **Interprétation** : Représente une absence totale de relations ou d’interactions entre les individus. En sciences sociales, cela peut indiquer un manque de communication ou de liens sociaux entre les acteurs concernés.

2. **“012” - Une arête asymétrique**

• **Signification** : Un seul lien directionnel existe entre deux nœuds ; le troisième nœud est isolé.

• **Interprétation** : Montre une relation unilatérale où un individu A influence ou communique avec un individu B, sans réciprocité, tandis que le troisième individu C n’est pas impliqué. Cela peut représenter une situation où l’information ou l’influence ne circule que dans un sens.

3. **“102” - Dyade mutuelle avec un nœud isolé**

• **Signification** : Un lien mutuel (réciproque) existe entre deux nœuds ; le troisième nœud est isolé.

• **Interprétation** : Indique une relation bidirectionnelle forte entre deux individus A et B (par exemple, une amitié réciproque), tandis que le troisième individu C n’est pas connecté. Cela souligne l’existence de sous-groupes ou de dyades au sein du réseau.

4. **“021D” - Étoile descendante**

• **Signification** : Un nœud envoie des liens directionnels à deux autres nœuds.

• **Interprétation** : Représente une structure où un individu A influence ou communique avec deux autres individus B et C, qui ne renvoient pas de liens à A ni entre eux. Cela peut symboliser une position de leadership ou d’autorité, où A est la source principale d’information ou d’influence.

5. **“021U” - Étoile montante**

• **Signification** : Deux nœuds envoient des liens directionnels vers un même nœud.

• **Interprétation** : Indique que deux individus B et C sont orientés vers un individu A, qui ne renvoie pas de liens. Cela peut représenter une situation où A est une figure centrale recevant de l’information, du soutien ou des demandes de B et C.

6. **“021C” - Chaîne linéaire**

• **Signification** : Un nœud A envoie un lien à B, qui envoie un lien à C.

• **Interprétation** : Illustre une séquence de relations ou de communication, où l’influence ou l’information se propage de A à B, puis de B à C. Cela peut représenter une chaîne de commandement ou la diffusion d’informations à travers des intermédiaires.

7. **“111D” - Dyade mutuelle avec un lien sortant**

• **Signification** : Deux nœuds A et B sont en relation mutuelle, et l’un d’eux (par exemple A) envoie un lien à un troisième nœud C.

• **Interprétation** : Représente un duo fortement connecté qui influence ou communique avec un troisième individu. Peut indiquer une coalition ou une alliance exerçant une influence externe.

8. **“111U” - Dyade mutuelle avec un lien entrant**

• **Signification** : Deux nœuds A et B sont en relation mutuelle, et ils reçoivent un lien d’un troisième nœud C.

• **Interprétation** : Montre qu’un individu C cherche à se connecter ou à influencer un duo étroitement lié. Cela peut refléter des dynamiques d’intégration ou d’influence ascendante.

9. **“030T” - Triade transitive**

• **Signification** : Liens directionnels de A à B, de B à C, et de A à C.

• **Interprétation** : Représente une structure hiérarchique transitive où l’influence ou l’information se propage de manière ordonnée. En sciences sociales, cela peut symboliser une chaîne de commandement efficace ou une hiérarchie claire.

10. **“030C” - Triade cyclique**

• **Signification** : Liens directionnels de A à B, de B à C, et de C à A.

• **Interprétation** : Illustre une boucle de relations où chaque individu influence le suivant, créant un cycle. Cela peut indiquer des relations réciproques complexes ou des cycles de dépendance et d’interaction.

11. **“201” - Dyade mutuelle avec un nœud isolé**

• **Signification** : Un lien mutuel existe entre deux nœuds ; le troisième nœud est isolé.

• **Interprétation** : Similaire à “102”, cela souligne une relation réciproque forte entre deux individus, avec un troisième individu non connecté. Peut mettre en évidence des sous-groupes au sein du réseau.

12. **“120D” - Triade mutuelle descendante**

• **Signification** : Un lien mutuel entre A et B, et A envoie un lien à C.

• **Interprétation** : Représente un duo A-B en relation réciproque, où A exerce une influence supplémentaire sur C. Cela peut indiquer une dynamique où un membre du duo a une position de leadership ou d’influence externe.

13. **“120U” - Triade mutuelle montante**

• **Signification** : Un lien mutuel entre A et B, et C envoie un lien à A.

• **Interprétation** : Montre qu’un individu C cherche à influencer ou se connecter avec un membre d’un duo A-B. Cela peut refléter des dynamiques d’accès ou d’ascension sociale.

14. **“120C” - Triade mutuelle cyclique**

• **Signification** : Un lien mutuel entre A et B, B envoie un lien à C, et C envoie un lien à A.

• **Interprétation** : Illustre des relations complexes avec des interactions mutuelles et asymétriques, formant un cycle. Peut représenter des réseaux d’influence où les relations sont interdépendantes.

15. **“210” - Triade quasi-complète**

• **Signification** : Deux liens mutuels entre les nœuds, et un lien asymétrique entre les deux autres nœuds.

• **Interprétation** : Indique un réseau fortement connecté avec des relations réciproques, mais où une relation n’est pas entièrement mutuelle. Cela peut signaler des déséquilibres de pouvoir ou d’influence au sein d’un groupe restreint.

16. **“300” - Triade complète**

• **Signification** : Trois liens mutuels existent entre les trois nœuds ; chaque nœud est en relation mutuelle avec les deux autres.

• **Interprétation** : Représente le niveau maximal de connectivité et de réciprocité dans une triade. En sciences sociales, cela peut symboliser un groupe très cohésif avec des interactions fortes et équilibrées entre tous les membres.

  

Ces triades permettent d’analyser les structures microscopiques au sein des réseaux sociaux. Elles aident à comprendre les dynamiques relationnelles, les positions d’influence, et les schémas d’interaction qui peuvent émerger dans les groupes sociaux. En étudiant la fréquence et le type de triades dans un réseau, les chercheurs peuvent déduire des propriétés globales du réseau, telles que la cohésion, la hiérarchie, et la présence de sous-groupes ou de cliques.

L'analyse des triades nous permet de comprendre les motifs relationnels présents dans le réseau. Par exemple, un nombre élevé de triades de type **030T** (une hiérarchie linéaire) peut indiquer une structure hiérarchique forte.

### 2.2 Mesure de la Transitivité et de la Réciprocité

#### 2.2.1 Transitivité

La transitivité mesure la probabilité que les relations soient transitives dans le réseau. En R, nous pouvons calculer le coefficient de clustering global et local.

```R
# Coefficient de clustering global
global_transitivity <- transitivity(g, type = "global")
print(global_transitivity)

# Coefficient de clustering local pour chaque nœud
local_transitivity <- transitivity(g, type = "local")
print(local_transitivity)
```

Le **coefficient de clustering global** mesure la probabilité qu'un nœud connecté à deux autres nœuds soit également connecté directement à ces deux nœuds entre eux, formant ainsi une triade fermée (un triangle). Il est calculé comme suit :

$$
C_{\text{global}} = \frac{\text{nombre de triangles} \times 3}{\text{nombre de triplets connectés}}

$$
- **Nombre de triangles** : Le nombre total de triades fermées dans le réseau.
- **Nombre de triplets connectés** : Le nombre total de triplets (ensembles de trois nœuds où au moins deux nœuds sont connectés).

**Interprétation :**

- **Valeur proche de 1** : Indique un réseau hautement clusterisé, où les nœuds ont tendance à former des groupes étroitement connectés. Cela signifie que si deux nœuds sont connectés à un même nœud, il est très probable qu'ils soient également connectés entre eux.
- **Valeur proche de 0** : Indique un réseau peu clusterisé, où les triades fermées sont rares. Les connexions sont plus aléatoires et il y a peu de cohésion locale.

**Coefficient de Clustering Local**

Le **coefficient de clustering local** pour un nœud individuel mesure la proportion des connexions possibles entre ses voisins qui sont effectivement réalisées. Il est calculé pour un nœud \( v \) comme :

$$
C_v = \frac{2e_v}{k_v(k_v - 1)}
$$

- \( e_v \) : Nombre de liens existants entre les voisins du nœud \( v \).
- \( k_v \) : Degré du nœud \( v \) (nombre de voisins directs).

**Interprétation :**

- **Valeur de \( C_v \) proche de 1** : Les voisins du nœud \( v \) sont fortement connectés entre eux, formant une structure de type clique autour de \( v \).
- **Valeur de \( C_v \) proche de 0** : Les voisins du nœud \( v \) sont peu ou pas connectés entre eux.

**Implications Pratiques**

- **Diffusion de l'Information** : Dans un réseau avec faible clustering, la diffusion de l'information est moins efficace à travers des boucles locales. Elle dépend davantage des connexions directes ou des chemins plus longs.

- **Robustesse du Réseau** : Un réseau peu clusterisé peut être moins robuste face à la défaillance de nœuds, car il n'y a pas de redondance des chemins entre les nœuds.

- **Stratégies d'Intervention** : Si l'objectif est d'augmenter la cohésion sociale ou la diffusion de l'information, il pourrait être bénéfique de **renforcer les connexions entre les voisins** des nœuds clés pour augmenter le clustering.

**Visualisation des Distributions** : Créez des histogrammes des valeurs de `local_transitivity` pour visualiser la distribution des coefficients de clustering locaux.

```R
hist(local_transitivity, breaks = 20, main = "Distribution du Coefficient de Clustering Local", xlab = "Coefficient de Clustering Local", ylab = "Fréquence")
```

**Identification des Nœuds Clés** : Repérez les nœuds avec des valeurs élevées de clustering local pour étudier leur rôle dans le réseau.

**Comparaison avec des Modèles Aléatoires** : Comparez le coefficient de clustering global de votre réseau avec celui d'un réseau aléatoire de même taille et même distribution de degrés pour déterminer si le clustering observé est significatif.

**Analyse de Communautés** : Utilisez des méthodes de détection de communautés pour voir s'il existe des sous-structures non évidentes malgré le faible clustering.

Les résultats du coefficient de clustering global et local renforcent l'observation que le réseau est **faiblement clusterisé** et manque de **cohésion locale**. Cela est cohérent avec le recensement des triades, qui montre une prédominance de triades ouvertes (sans liens entre tous les nœuds). Cette structure a des implications sur la dynamique du réseau, notamment en termes de diffusion de l'information, de formation de communautés et de résilience du réseau.

#### 2.2.2 Réciprocité

**Interprétation des résultats de la réciprocité dans un réseau**

La **réciprocité** est une mesure fondamentale dans l'analyse des réseaux dirigés, car elle quantifie la proportion de liens mutuels par rapport au nombre total de liens dans le réseau. Une compréhension approfondie de la réciprocité peut révéler des informations clés sur la structure sociale et les dynamiques d'interaction au sein du réseau.


Dans un **réseau dirigé**, les liens ont une direction, ce qui signifie que si un nœud \( A \) est lié à un nœud \( B \), cela ne garantit pas que \( B \) est lié à \( A \). La **réciprocité** mesure la tendance des relations à être mutuelles. Elle est définie comme :

- **Réciprocité dyadique** : La proportion de paires de nœuds avec des liens mutuels par rapport au nombre total de paires liées.
- **Réciprocité des arêtes** : La proportion de liens réciproques par rapport au nombre total de liens dans le réseau.

**Formule :**

Pour un réseau dirigé \( G \) avec \( L \) liens, la réciprocité \( r \) est calculée comme :

$$
r = \frac{\text{Nombre de paires de nœuds avec des liens mutuels}}{\text{Nombre total de paires de nœuds avec au moins un lien}}

$$
Ou, pour la réciprocité des arêtes :

$$
r = \frac{\text{Nombre de liens réciproques}}{L}
$$
**Calcul de la Réciprocité en R**

Dans le package **igraph**, la fonction `reciprocity()` permet de calculer la réciprocité d'un réseau.

```R
# Calcul de la réciprocité du réseau
network_reciprocity <- reciprocity(g)
print(network_reciprocity)
```

Par défaut, la fonction `reciprocity()` calcule la réciprocité des arêtes, mais elle peut également calculer la réciprocité dyadique en spécifiant le paramètre `mode`.

```R
# Réciprocité dyadique
dyadic_reciprocity <- reciprocity(g, mode = "ratio")
print(dyadic_reciprocity)
```

**Réciprocité des Arêtes**

- **Valeur de `network_reciprocity` proche de 1** : Indique que la plupart des liens sont réciproques. Si un nœud \( A \) est connecté à un nœud \( B \), il est très probable que \( B \) soit également connecté à \( A \).
- **Valeur proche de 0** : Indique que les liens sont majoritairement unidirectionnels. La réciprocité est faible.

**Réciprocité Dyadique**

- **Valeur de `dyadic_reciprocity` proche de 1** : La plupart des paires de nœuds connectés ont des liens mutuels.
- **Valeur proche de 0** : Peu de paires de nœuds ont des liens mutuels.

Une **Faible Réciprocité** peut indiquer une **structure hiérarchique**, où les interactions sont principalement unidirectionnelles. Par exemple, dans une organisation avec une chaîne de commandement stricte. Les informations ou les ressources circulent principalement dans une direction. Les relations mutuelles étant rares, cela peut refléter un manque de confiance ou de collaboration.

A l'inverse, une **Haute Réciprocité** montre que les membres du réseau interagissent mutuellement, ce qui peut renforcer les liens sociaux. Les relations plus équilibrées entre les nœuds **facilitent la Diffusion** des informations où les ressources peuvent circuler plus librement dans le réseau.

**Analyse Approfondie**

Pour mieux comprendre la réciprocité dans votre réseau, vous pouvez analyser la distribution des liens réciproques entre les nœuds.

```R
# Calculer le nombre de relations entrantes et sortantes pour chaque nœud
in_degree <- degree(g, mode = "in")
out_degree <- degree(g, mode = "out")

# Identifier les nœuds avec des liens réciproques
recip_edges <- which_mutual(g)

# Nombre total de liens réciproques
total_recip_edges <- length(recip_edges) / 2  # Chaque lien réciproque est compté deux fois
print(total_recip_edges)

# Créer un vecteur pour la couleur des arêtes
edge_colors <- ifelse(is.mutual(g), "red", "gray")

# Visualiser le réseau
plot(g, edge.arrow.size = 0.5, vertex.color = "lightblue", vertex.size = 30,
     vertex.label.cex = 1.2, edge.color = edge_colors)
     
```

**Par rapport au hasard ?**

Pour déterminer si le niveau de réciprocité observé est significatif, vous pouvez comparer votre réseau avec un **réseau aléatoire de même taille et même densité**.

```R
# Générer un réseau aléatoire avec la même taille et densité
g_random <- erdos.renyi.game(vcount(g), ecount(g), type = "gnm", directed = TRUE)

# Calculer la réciprocité du réseau aléatoire
random_reciprocity <- reciprocity(g_random)
print(random_reciprocity)
```

- **Si la réciprocité du réseau réel est supérieure** à celle du réseau aléatoire, cela suggère que les liens réciproques sont plus fréquents que ce qui serait attendu par hasard.
- **Si elle est similaire ou inférieure**, cela indique que la réciprocité dans le réseau n'est pas significativement différente de ce qui serait attendu dans un réseau aléatoire.
**Étude des Sous-Groupes**

Analysez si certains sous-groupes du réseau présentent une réciprocité plus élevée.

```R
# Détection de communautés
communities <- cluster_louvain(as.undirected(g))

# Analyser la réciprocité au sein de chaque communauté
for (i in 1:length(communities)) {
  subgraph_nodes <- communities[[i]]
  subgraph <- induced_subgraph(g, subgraph_nodes)
  subgraph_reciprocity <- reciprocity(subgraph)
  cat("Réciprocité de la communauté", i, ":", subgraph_reciprocity, "\n")
}
```

**Temporalité des Données**

Si les données le permettent, analysez la réciprocité au fil du temps pour voir si elle augmente ou diminue, ce qui peut indiquer des changements dans la dynamique du réseau.

**Corrélation avec d'Autres Mesures**

Examinez la corrélation entre la réciprocité et d'autres mesures, comme la centralité des nœuds, pour voir si les nœuds les plus centraux ont tendance à avoir des relations plus réciproques.

La réciprocité est une mesure clé pour comprendre la **dynamique relationnelle** au sein d'un réseau dirigé. Dans votre réseau, les résultats indiquent une **faible réciprocité**, suggérant que les relations sont majoritairement unidirectionnelles. Cela peut refléter une **structure hiérarchique**, un **manque de cohésion sociale** ou des **interactions asymétriques**.

#### 2.2.3 Fonction Boostrap d'analyse de réciptocité et de Transivité

Voilà une fonction générale de comparaison de réciprocité et transitivité d'un réseau`netranseval` et effectue une analyse bootstrap de la réciprocité et de la transitivité sur des réseaux aléatoires de type Erdos-Rényi et Barabasi-Albert. Si le paramètre `type` est défini sur `'Erdos'` ou `'Barabasi'`, la fonction conserve la même structure de sortie mais avec des valeurs `NA` pour les coefficients non calculés.

```R
netranseval <- function(g, n, type = 'ALL') {
  # Charger la bibliothèque nécessaire
  if (!requireNamespace("igraph", quietly = TRUE)) {
    install.packages("igraph")
  }
  library(igraph)
  
  # Valider le paramètre 'type'
  if (!(type %in% c('Erdos', 'Barabasi', 'ALL'))) {
    stop("Le type doit être 'Erdos', 'Barabasi' ou 'ALL'")
  }
  
  # Obtenir les propriétés du graphe d'entrée
  nombre_noeuds <- vcount(g)
  nombre_aretes <- ecount(g)
  est_dirige <- is_directed(g)
  
  # Calculer la transitivité et la réciprocité du graphe d'entrée
  trans_input <- transitivity(g, type = "global")
  recip_input <- reciprocity(g)
  
  # Initialiser les variables pour stocker les résultats
  trans_erdos <- NA
  recip_erdos <- NA
  trans_barabasi <- NA
  recip_barabasi <- NA
  
  # Générer les graphes d'Erdos-Rényi
  if (type == 'Erdos' || type == 'ALL') {
    trans_erdos_values <- numeric(n)
    recip_erdos_values <- numeric(n)
    for (i in 1:n) {
      # Générer un graphe Erdos-Rényi avec le même nombre de nœuds et d'arêtes
      g_erdos <- sample_gnm(n = nombre_noeuds, m = nombre_aretes, directed = est_dirige, loops = FALSE)
      
      # Calculer la transitivité et la réciprocité
      trans_erdos_values[i] <- transitivity(g_erdos, type = "global")
      recip_erdos_values[i] <- reciprocity(g_erdos)
    }
    # Calculer la moyenne
    trans_erdos <- mean(trans_erdos_values, na.rm = TRUE)
    recip_erdos <- mean(recip_erdos_values, na.rm = TRUE)
  }
  
  # Générer les graphes de Barabasi-Albert
  if (type == 'Barabasi' || type == 'ALL') {
    trans_barabasi_values <- numeric(n)
    recip_barabasi_values <- numeric(n)
    
    # Déterminer le paramètre 'm' pour sample_pa
    m <- max(1, round(nombre_aretes / nombre_noeuds))
    
    for (i in 1:n) {
      # Générer un graphe de Barabasi-Albert
      g_barabasi <- sample_pa(n = nombre_noeuds, power = 1, m = m, directed = est_dirige)
      
      # Calculer la transitivité et la réciprocité
      trans_barabasi_values[i] <- transitivity(g_barabasi, type = "global")
      recip_barabasi_values[i] <- reciprocity(g_barabasi)
    }
    # Calculer la moyenne
    trans_barabasi <- mean(trans_barabasi_values, na.rm = TRUE)
    recip_barabasi <- mean(recip_barabasi_values, na.rm = TRUE)
  }
  
  # Préparer le résultat avec la même structure
  resultat <- c(
    transitivite = trans_input,
    reciprocite = recip_input,
    erdos_coefficient_transitivite = trans_input/trans_erdos,
    erdos_coefficient_reciprocite = recip_input/recip_erdos,
    barabasi_coefficient_transitivite = trans_input/trans_barabasi,
    barabasi_coefficient_reciprocite = recip_input/recip_barabasi
  )
  
  return(resultat)
}
```

**Explication de la Fonction**

**Génération et Analyse des Graphes Erdos-Rényi :**

   - Si `type` est `'Erdos'` ou `'ALL'`, la fonction génère `n` graphes Erdos-Rényi avec le même nombre de nœuds et d'arêtes que le graphe d'entrée.
   - Pour chaque graphe généré, elle calcule la transitivité et la réciprocité.
   - Les moyennes de ces mesures sont calculées et stockées.

**Génération et Analyse des Graphes Barabasi-Albert :**

   - Si `type` est `'Barabasi'` ou `'ALL'`, la fonction génère `n` graphes Barabasi-Albert.
   - Le paramètre `m` est déterminé pour approcher le nombre d'arêtes du graphe d'entrée.
   - Pour chaque graphe généré, elle calcule la transitivité et la réciprocité.
   - Les moyennes de ces mesures sont calculées et stockées.

In fine la reciprocité et la transivité du réseau sont rapportées à ces valeurs moyennes dû au hasard. Une valeur est supérieur ou inférieur à 1 pour savoir si le réseau est plus ou moins transitif et réciproque que le hasard.

**Exemple d'Utilisation**

Cas 1 : Type 'ALL'

```R
# Effectuer l'analyse avec 100 itérations pour les deux types de graphes aléatoires
resultat_all <- analyse_reseau_aleatoire(g_exemple, n = 100, type = 'ALL')

# Afficher les résultats
print(resultat_all)
```

Cas 2 : Type 'Erdos'

```R
# Effectuer l'analyse avec 100 itérations uniquement pour les graphes Erdos-Rényi
resultat_erdos <- analyse_reseau_aleatoire(g_exemple, n = 100, type = 'Erdos')

# Afficher les résultats
print(resultat_erdos)
```

Cas 3 : Type 'Barabasi'

```R
# Effectuer l'analyse avec 100 itérations uniquement pour les graphes Barabasi-Albert
resultat_barabasi <- analyse_reseau_aleatoire(g_exemple, n = 100, type = 'Barabasi')

# Afficher les résultats
print(resultat_barabasi)
```

**Résultat :**

- Les coefficients relatifs aux graphes Erdos-Rényi sont présents mais contiennent des valeurs `NA`.

### 2.3 Modélisation Statistique des Triades : Modèles Exponentiels Aléatoires de Graphes (ERGMs)

Les ERGMs sont des modèles statistiques qui permettent de modéliser la formation des liens dans un réseau en fonction de différentes caractéristiques, y compris les triades, la transitivité et la réciprocité.

Nous utiliserons le package **statnet**, en particulier les packages **ergm** et **network**.

```R
# Installation et chargement des packages
install.packages("statnet")
library(statnet)

# Conversion du graphe igraph en objet network
g_network <- asNetwork(g)

# Spécification du modèle ERGM
# Nous incluons les termes pour la densité, la réciprocité et la transitivité
model <- ergm(g_network ~ edges + mutual + transitive)

# Ajustement du modèle
fit <- ergm(model)

# Résumé du modèle
summary(fit)
```

Les coefficients estimés indiquent l'influence de chaque paramètre sur la probabilité de formation des liens. Un coefficient positif pour la réciprocité suggère que les liens mutuels sont plus probables qu'attendus par hasard.
## Partie 3 : Applications en Sciences Sociales

L'analyse des triades, de la transitivité et de la réciprocité, ainsi que l'utilisation des Modèles Exponentiels Aléatoires de Graphes (ERGM), ont révolutionné la façon dont les chercheurs en sciences sociales comprennent et modélisent les interactions sociales complexes. Ces concepts ont été appliqués dans divers domaines, tels que les réseaux d'amitié, les organisations, les réseaux criminels et politiques, pour explorer comment les individus et les groupes se connectent et interagissent. Dans cette partie, nous examinerons en détail plusieurs études de cas qui illustrent l'utilisation de ces concepts en recherche, en mettant l'accent sur leurs méthodes et designs de recherche.

### 3.1 Études des Réseaux d'Amitié et de Réciprocité

Les réseaux d'amitié, en particulier parmi les adolescents, offrent un terrain fertile pour explorer comment les relations sociales se forment et évoluent. **Goodreau, Kitts et Morris (2009)** ont mené une étude influente qui utilise les ERGM pour analyser les réseaux d'amitié chez les adolescents, en se concentrant sur la façon dont la transitivité et la réciprocité influencent la formation des liens.

#### Méthodes et Design de Recherche

- **Objectif de l'étude**: Examiner comment les attributs individuels et les structures relationnelles influencent la formation des amitiés chez les adolescents.

- **Population étudiée**: Les données proviennent de l'Add Health Study, une enquête longitudinale nationale aux États-Unis qui collecte des informations sur les réseaux sociaux des élèves du secondaire.

- **Collecte des données**:

  - **Procédure**: Les élèves ont été invités à nommer jusqu'à cinq amis masculins et cinq amis féminins, créant ainsi des réseaux dirigés où les liens représentent des nominations d'amitié.
  
  - **Variables mesurées**:
    - **Attributs individuels**: Sexe, âge, appartenance ethnique, niveau scolaire, etc.
    - **Liens d'amitié**: Nominations d'amis, permettant de construire la matrice d'adjacence du réseau.

- **Analyse des données**:

  - **Construction du réseau**: Les données de nominations ont été utilisées pour construire des réseaux sociaux pour chaque école participante.
  
  - **Application des ERGM**: Les auteurs ont utilisé des Modèles Exponentiels Aléatoires de Graphes pour modéliser la probabilité de formation des liens d'amitié en fonction des attributs individuels et des effets structurels tels que la réciprocité et la transitivité.
  
  - **Variables incluses dans le modèle**:
    - **Effets d'attributs**: Homophilie basée sur le sexe, l'âge, l'appartenance ethnique, etc.
    - **Effets structurels**: Réciprocité des liens, transitivité (formation de triades fermées), popularité et activité des nœuds.

#### Résultats et Interprétation

- **Homophilie**: Les résultats ont montré une forte tendance à l'homophilie, les élèves étant plus susceptibles de nommer des amis du même sexe, de la même ethnie et du même niveau scolaire.

- **Réciprocité**: Les liens d'amitié étaient significativement réciproques, ce qui reflète la nature mutuelle des relations d'amitié à l'adolescence.

- **Transitivité**: Une forte transitivité a été observée, indiquant que les élèves sont plus susceptibles d'être amis avec les amis de leurs amis, formant ainsi des triades fermées.

- **Implications**: L'étude suggère que les processus sociaux locaux, tels que la réciprocité et la transitivité, jouent un rôle crucial dans la formation des réseaux d'amitié, en interaction avec les similitudes d'attributs individuels.

### 3.2 Réseaux de Collaboration dans les Organisations

Comprendre les réseaux de collaboration au sein des organisations est essentiel pour améliorer l'efficacité opérationnelle et la cohésion du personnel. **Lomi et Pattison (2006)** ont exploré les fondements organisationnels de la structure des réseaux en examinant comment les relations de collaboration se forment entre les employés.

#### Méthodes et Design de Recherche

- **Contexte**: L'étude a été menée dans une grande entreprise manufacturière italienne.

- **Collecte des données**:

  - **Procédure**: Des questionnaires ont été distribués aux employés pour recueillir des informations sur leurs relations de collaboration. Les employés ont identifié avec qui ils collaboraient régulièrement.
  
  - **Variables mesurées**:
    - **Attributs individuels**: Département, ancienneté, niveau hiérarchique, etc.
    - **Liens de collaboration**: Indications des relations de travail régulières.

- **Analyse des données**:

  - **Construction du réseau**: Un réseau dirigé a été construit, où les liens représentent l'indication par un employé qu'il collabore avec un autre.
  
  - **Application des ERGM**: Les auteurs ont utilisé les ERGM pour modéliser la formation des liens de collaboration en tenant compte des effets des attributs individuels et des structures relationnelles.

- **Variables incluses dans le modèle**:

  - **Effets d'attributs**: Même département, même niveau hiérarchique, proximité géographique.
  
  - **Effets structurels**: Réciprocité, transitivité, effets de popularité (certains employés recevant plus de nominations), effets d'activité (certains employés nommant plus de collaborateurs).

#### Résultats et Interprétation

- **Réciprocité**: Les liens de collaboration étaient souvent réciproques, reflétant des relations de travail mutuelles.

- **Transitivité**: Une tendance significative à la formation de triades fermées a été observée, suggérant que les employés collaborent avec les collaborateurs de leurs collaborateurs.

- **Effets des attributs**: La collaboration était plus probable entre les employés du même département et du même niveau hiérarchique.

- **Implications**: L'étude souligne l'importance des structures organisationnelles formelles et des processus sociaux informels dans la formation des réseaux de collaboration. Les ERGM ont permis de distinguer les effets des attributs individuels de ceux des structures relationnelles.

### 3.3 Réseaux Criminels et Formation des Triades

Les réseaux criminels présentent des structures complexes où la confiance et la loyauté sont essentielles. **Papachristos et al. (2013)** ont étudié comment les relations sociales dans les gangs de rue influencent le risque de blessure par arme à feu, en utilisant l'analyse des réseaux sociaux.

#### Méthodes et Design de Recherche

- **Contexte**: L'étude a été menée à Chicago, une ville avec une histoire de violence liée aux gangs.

- **Collecte des données**:

  - **Sources**: Données policières sur les arrestations conjointes (co-arrestations), indiquant que deux individus ont été arrêtés ensemble pour le même incident.
  
  - **Variables mesurées**:
    - **Attributs individuels**: Appartenance à un gang, âge, antécédents criminels.
    - **Liens sociaux**: Relations basées sur les co-arrestations, considérées comme indicateurs de relations criminelles.

- **Analyse des données**:

  - **Construction du réseau**: Un réseau non dirigé où les liens représentent des co-arrestations.
  
  - **Application des ERGM**: Les auteurs ont utilisé les ERGM pour modéliser la probabilité de formation des liens en fonction des attributs individuels et des structures de réseau.

- **Variables incluses dans le modèle**:

  - **Effets d'attributs**: Même gang, proximité géographique.
  
  - **Effets structurels**: Triades fermées (transitivité), degrés des nœuds (centralité).

#### Résultats et Interprétation

- **Transitivité**: Les triades fermées étaient fréquentes, suggérant que les membres de gangs opèrent souvent en petits groupes cohésifs.

- **Centralité et risque**: Les individus occupant des positions centrales dans le réseau (avec de nombreux liens) avaient un risque accru de blessure par arme à feu.

- **Implications**: L'étude démontre que les structures de réseau influencent non seulement la dynamique interne des gangs, mais aussi les risques auxquels les individus sont exposés. Les ERGM ont permis de comprendre comment les attributs individuels et les structures relationnelles contribuent à ces risques.

### 3.4 Étude des Triades et de la Transitivité dans les Réseaux Politiques

Les relations internationales et les alliances politiques sont influencées par des dynamiques complexes. **Cranmer et Desmarais (2011)** ont utilisé les ERGM pour analyser les réseaux d'alliances entre pays, en examinant comment la transitivité et les similarités idéologiques influencent la formation des alliances.

#### Méthodes et Design de Recherche

- **Contexte**: Les alliances militaires entre pays sur une période historique donnée.

- **Collecte des données**:

  - **Sources**: Bases de données internationales sur les traités et alliances, comme la Correlates of War (COW) Alliance Dataset.
  
  - **Variables mesurées**:
    - **Attributs des pays**: Régime politique, puissance militaire, alignement idéologique.
    - **Liens d'alliance**: Existence de traités d'alliance militaire entre pays.

- **Analyse des données**:

  - **Construction du réseau**: Un réseau non dirigé où les liens représentent des alliances militaires.
  
  - **Application des ERGM**: Les ERGM ont été utilisés pour modéliser la probabilité de formation des alliances en fonction des attributs nationaux et des structures de réseau.

- **Variables incluses dans le modèle**:

  - **Effets d'attributs**: Similarité idéologique, proximité géographique, intérêts stratégiques.
  
  - **Effets structurels**: Transitivité (triades fermées), degrés des nœuds (nombre d'alliances d'un pays).

#### Résultats et Interprétation

- **Transitivité**: Les pays étaient plus susceptibles de former des alliances avec les alliés de leurs alliés, indiquant un effet de transitivité significatif.

- **Homophilie idéologique**: Les pays avec des régimes politiques similaires (par exemple, démocraties) étaient plus susceptibles de s'allier.

- **Effets structurels**: Les pays déjà bien connectés (avec de nombreuses alliances) étaient plus susceptibles de former de nouvelles alliances, suggérant un effet de popularité cumulative.

- **Implications**: L'étude montre que les structures de réseau et les attributs nationaux interagissent pour façonner les relations internationales. Les ERGM fournissent un cadre pour modéliser ces dynamiques complexes.

### 3.5 Réseaux de Diffusion de l'Information

Les réseaux sociaux en ligne jouent un rôle crucial dans la propagation de l'information, des idées et des comportements. L'analyse des triades, de la transitivité et de la réciprocité permet de comprendre comment ces processus de diffusion sont influencés par la structure du réseau. **Centola (2010)** et **Ugander et al. (2012)** ont mené des études significatives dans ce domaine, en utilisant des méthodes de modélisation avancées pour explorer la dynamique de la diffusion de l'information.

#### Méthodes et Design de Recherche

- **Objectif de l'étude**:

  - **Centola (2010)** visait à déterminer comment la structure du réseau influence la propagation des comportements de santé en ligne.
  - **Ugander et al. (2012)** cherchaient à analyser la structure du réseau Facebook pour comprendre les mécanismes de diffusion de l'information.

- **Population étudiée**:

  - **Centola** a recruté des participants en ligne pour une expérience contrôlée.
  - **Ugander et al.** ont analysé les données de plusieurs millions d'utilisateurs de Facebook.

- **Collecte des données**:

  - **Procédure**:
    - **Centola** a créé un réseau social en ligne expérimental où les participants étaient assignés aléatoirement à des réseaux structurés différemment (réseaux à cluster élevé vs. réseaux aléatoires).
    - **Ugander et al.** ont utilisé les données internes de Facebook pour construire le graphe social des utilisateurs.

  - **Variables mesurées**:
    - **Adoption du comportement cible**: Participation des utilisateurs à une plateforme de santé en ligne (Centola).
    - **Structure du réseau**: Mesures de transitivité, de densité des triades, de degrés des nœuds (Ugander et al.).

- **Analyse des données**:

  - **Construction du réseau**:
    - **Centola** a manipulé la structure du réseau pour créer des conditions expérimentales contrôlées.
    - **Ugander et al.** ont construit un graphe social géant représentant les connexions entre les utilisateurs de Facebook.

  - **Application des ERGM**:
    - **Centola** n'a pas utilisé les ERGM, mais a mis l'accent sur l'impact de la structure du réseau sur la diffusion. **Grabowicz et al. (2012)** ont utilisé des ERGM pour modéliser la diffusion de l'information sur Twitter, en tenant compte de la transitivité et des triades.

  - **Variables incluses dans le modèle**:
    - **Effets structurels**: Transitivité, présence de triades fermées, réciprocité.
    - **Attributs individuels**: Influence sociale, activité en ligne, nombre d'amis.

#### Résultats et Interprétation

- **Effet de la transitivité**:

  - **Centola** a trouvé que les réseaux à forte transitivité (clusters élevés) favorisent une diffusion plus rapide et plus étendue des comportements de santé en ligne, en raison du renforcement social accru dans les triades fermées.

- **Rôle des triades**:

  - Les triades fermées augmentent la probabilité qu'un individu adopte un comportement si plusieurs de ses amis l'ont déjà adopté, illustrant l'importance de la pression sociale et du renforcement mutuel.

- **Réciprocité**:

  - **Grabowicz et al.** ont montré que la réciprocité dans les relations influence positivement la propagation de l'information, car les liens bidirectionnels renforcent la confiance et l'attention mutuelle.

### 3.6 Étude des Mouvements Sociaux

Les mouvements sociaux dépendent fortement des réseaux de relations entre les individus pour mobiliser les ressources, coordonner les actions et diffuser les idéologies. L'analyse des triades, de la transitivité et de la réciprocité offre des insights profonds sur la dynamique interne des mouvements sociaux. **Diani (2003)** et **Gonzalez-Bailon et al. (2013)** ont exploré ces aspects en profondeur.

#### Méthodes et Design de Recherche

- **Objectif de l'étude**:

  - **Diani (2003)** a examiné comment les réseaux personnels influencent la participation aux mouvements environnementaux.
  - **Gonzalez-Bailon et al. (2013)** ont étudié la diffusion de l'information lors des manifestations du mouvement "Indignados" en Espagne.

- **Population étudiée**:

  - **Diani** a étudié des militants environnementaux en Italie.
  - **Gonzalez-Bailon et al.** ont analysé les utilisateurs de Twitter impliqués dans les manifestations.

- **Collecte des données**:

  - **Procédure**:
    - **Diani** a mené des entretiens et des questionnaires pour recueillir des données sur les relations personnelles et l'engagement militant.
    - **Gonzalez-Bailon et al.** ont collecté des données Twitter en utilisant des hashtags associés au mouvement.

  - **Variables mesurées**:
    - **Liens sociaux**: Amitiés, collaborations, affiliations organisationnelles.
    - **Participation et influence**: Nombre de messages, retweets, centralité dans le réseau.

- **Analyse des données**:

  - **Construction du réseau**:
    - Les relations déclarées par les militants ont été utilisées pour construire des réseaux sociaux (Diani).
    - Les mentions et retweets sur Twitter ont été utilisées pour créer un graphe d'interactions (Gonzalez-Bailon et al.).

  - **Application des ERGM**:
    - **Diani** a utilisé des analyses de réseaux sociaux qualitatives et quantitatives, intégrant des éléments de transitivité et de réciprocité.
    - **Gonzalez-Bailon et al.** ont appliqué des ERGM pour modéliser la probabilité de formation des liens en fonction de la structure du réseau.

  - **Variables incluses dans le modèle**:
    - **Effets structurels**: Triades fermées, réciprocité, centralité.
    - **Attributs individuels**: Niveau d'engagement, affiliation organisationnelle, influence en ligne.

#### Résultats et Interprétation

- **Transitivité et mobilisation**:

  - **Diani** a constaté que les militants intégrés dans des triades fermées sont plus susceptibles de participer activement, en raison du soutien mutuel et de la pression sociale positive.

- **Réciprocité et coordination**:

  - **Gonzalez-Bailon et al.** ont démontré que la réciprocité des interactions en ligne augmente la diffusion des informations et facilite la coordination des actions collectives.

- **Effets des structures de réseau**:

  - Les individus occupant des positions centrales dans les triades et les structures réciproques sont souvent des leaders d'opinion ou des facilitateurs clés dans le mouvement.
### 3.6 Synthèse et Implications pour la Recherche

Les études présentées démontrent que les concepts de transitivité, de réciprocité et les ERGM sont des outils puissants pour analyser les réseaux sociaux dans divers contextes. En modélisant les probabilités de formation des liens en fonction des attributs individuels et des structures relationnelles, les chercheurs peuvent :

- **Distinguer les effets individuels et structurels**: Comprendre comment les caractéristiques personnelles interagissent avec les structures de réseau pour influencer les relations sociales.

- **Explorer les dynamiques locales**: Analyser comment les processus tels que la formation de triades et la réciprocité affectent la cohésion et la structure globale du réseau.

- **Prédire la formation de liens**: Utiliser les modèles pour prévoir où de nouveaux liens sont susceptibles de se former, ce qui est utile pour des applications pratiques comme le marketing viral ou l'intervention sociale.

- **Informer les politiques et les interventions**: Les connaissances sur les structures de réseau peuvent aider à concevoir des interventions ciblées pour influencer les comportements, réduire la criminalité ou améliorer la collaboration organisationnelle.

### Références

- **Cartwright, D., & Harary, F. (1956)**. Structural Balance: A Generalization of Heider's Theory. *Psychological Review*, 63(5), 277–293.
- **Centola, D. (2010)**. The Spread of Behavior in an Online Social Network Experiment. *Science*, 329(5996), 1194-1197.
- **Cranmer, S. J., & Desmarais, B. A. (2011)**. Inferential network analysis with exponential random graph models. *Political Analysis*, 19(1), 66-86.
- **Diani, M. (2003)**. *Social Movements and Networks: Relational Approaches to Collective Action*. Oxford University Press.
- **Gonzalez-Bailon, S., Borge-Holthoefer, J., Rivero, A., & Moreno, Y. (2013)**. The Dynamics of Protest Recruitment through an Online Network. *Scientific Reports*, 3, 1-7.
- **Goodreau, S. M., Kitts, J. A., & Morris, M. (2009)**. Birds of a Feather, Or Friend of a Friend? Using Exponential Random Graph Models to Investigate Adolescent Social Networks. *Demography*, 46(1), 103-125.
- **Grabowicz, P. A., Ramasco, J. J., Moro, E., Pujol, J. M., & Eguiluz, V. M. (2012)**. Social Features of Online Networks: The Strength of Intermediary Ties in Online Social Media. *PLoS ONE*, 7(1), e29358.
- **Lomi, A., & Pattison, P. E. (2006)**. Manufacturing relations: An empirical study of the organizational foundations of network structure. *Social Networks*, 28(4), 349-367.
- **Papachristos, A. V., Braga, A. A., & Hureau, D. M. (2013)**. Social networks and the risk of gunshot injury. *Journal of Urban Health*, 90(5), 992-1003.
- **Snijders, T. A., Pattison, P., Robins, G. L., & Handcock, M. S. (2006)**. New specifications for exponential random graph models. *Sociological Methodology*, 36(1), 99-153.
- **Ugander, J., Karrer, B., Backstrom, L., & Marlow, C. (2011)**. The Anatomy of the Facebook Social Graph. *arXiv preprint arXiv:1111.4503*.
- **Wasserman, S., & Faust, K. (1994)**. *Social Network Analysis: Methods and Applications*. Cambridge University Press.