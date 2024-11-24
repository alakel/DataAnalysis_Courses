Les dynamiques de réseau abordent la question des changements d’état des nœuds et des liens dans un réseau au cours du temps. Ce champ est essentiel pour comprendre comment les structures relationnelles évoluent, influencent la diffusion d’informations, d’épidémies, de comportements, et plus généralement, comment les liens sociaux et autres réseaux se reconfigurent. Cette séance couvre dans un 1er temps modèles de propagation d’épidémies et de comportements. Un autre cours (11B) sera consacré aux modèles plus complexes tels que les SAOM et les TERGM.

---

# I. Théories de la dynamique des réseaux

## 1.1. Modèles de Propagation en Épidémiologie

Les modèles de propagation sont essentiels pour comprendre la diffusion des maladies, mais aussi pour modéliser d'autres types de processus de contagion, tels que les comportements ou les informations dans des populations humaines ou animales. La dynamique de propagation repose sur des schémas simples de transitions d'état des entités et de leur relations qui permettent d'illustrer comment un message (virus, rumeur, comportement) se diffuse dans un réseau d'Agents en relation les un avec les autres.

Les modèles de propagation, notamment les modèles SIR, SIS et SIRS, sont construits pour comprendre comment une épidémie se propage dans une population, en s'appuyant sur des compartiments définis par l'état des individus.

### Modèle SIR : Susceptible-Infected-Recovered

Le modèle SIR, introduit par **Kermack et McKendrick en 1927**, est l'un des modèles les plus basiques mais puissants pour décrire la propagation d'une épidémie. Ce modèle suppose que chaque individu dans la population se trouve dans un des trois états suivants : 

- **S (Susceptible)** : Les individus sont susceptibles d'être infectés.  
- **I (Infected)** : Les individus sont infectés et peuvent transmettre la maladie.
- **R (Recovered)** : Les individus ont récupéré et sont immunisés, ne pouvant plus être infectés ni transmettre la maladie.

Dans ce modèle, les individus suivent un parcours linéaire et sans retour : 

1. Un individu passe de S à I lorsqu'il entre en contact avec un infecté, avec une probabilité de transmission définie par un taux de transmission, \(\beta\).
2. Les infectés passent à l'état R au bout d'un certain temps, représentant la période de récupération, avec un taux de guérison \(\gamma\).

Le modèle est formalisé par un système d'équations différentielles :
$$
\frac{dS}{dt} = -\beta \frac{SI}{N}
$$
$$
\frac{dI}{dt} = \beta \frac{SI}{N} - \gamma I
$$
$$
\frac{dR}{dt} = \gamma I
$$

Où :
- \(N\) est la taille totale de la population.
- \(\beta\) est le taux de transmission.
- \(\gamma\) est le taux de guérison.

Le **nombre de reproduction de base**
$$
R_0 = \frac{\beta}{\gamma}
$$
est un indicateur clé dans ce modèle. Si \(R_0 > 1\), l'infection peut potentiellement se transformer en épidémie, car chaque individu infecté contamine plus d’une personne en moyenne. Si \(R_0 < 1\), l'infection tend à s'éteindre.

### Modèle SIS : Susceptible-Infected-Susceptible

Le modèle SIS est une variante du modèle SIR, adaptée aux maladies pour lesquelles les individus ne développent pas d'immunité après infection (comme le rhume). Dans ce modèle :

1. Les individus passent de S à I lorsqu'ils sont exposés à des infectés, avec une probabilité \(\beta\).
2. Les individus infectés peuvent redevenir susceptibles après récupération, avec un taux de récupération \(\gamma\).

Les équations différentielles pour ce modèle sont :
$$
\frac{dS}{dt} = \gamma I - \beta \frac{SI}{N}
$$
$$
\frac{dI}{dt} = \beta \frac{SI}{N} - \gamma I
$$
Ici, le système peut atteindre un équilibre endémique où l'infection persiste dans la population à un niveau stable. Ce modèle est pertinent pour des maladies où la réinfection est fréquente.

**Simulation de Diffusion**

La simulation des modèles de diffusion repose sur l'implémentation des règles de transition d'état et permet d'observer des phénomènes comme le pic de l’épidémie, la durée de l'infection dans le réseau, et les effets de la structure de réseau sur la propagation.

1. **Initialisation** : Définir l'état initial de chaque nœud (par exemple, 95 % susceptibles, 5 % infectés) et les paramètres du modèle (\(\beta\) et \(\gamma\)).

2. **Transition d'État** : À chaque unité de temps, chaque nœud infecté a une probabilité de \(\beta\) de transmettre l'infection à ses voisins susceptibles. Chaque nœud infecté a une probabilité \(\gamma\) de se rétablir (SIR) ou de revenir à l'état S (SIS).

3. **Itération** : Répéter les étapes jusqu'à atteindre un état stable ou une condition d’arrêt (par exemple, 90 % de la population dans l’état R).

4. **Observation des Résultats** : Analyser les données de simulation, telles que le nombre maximum d’infectés simultanés, la vitesse de propagation, et le nombre total de récupérés.

### Modèle SIR Hétérogène : Division en Sous-Groupes

Dans un modèle SIR classique, nous avons trois équations différentielles qui modélisent les compartiments Susceptible (\(S\)), Infecté (\(I\)) et Récupéré (\(R\)) dans une population homogène. Avec une population hétérogène, nous introduisons plusieurs sous-populations, chacune ayant ses propres équations et paramètres.

Par exemple, si l’on divise la population en deux groupes (par exemple, jeunes et personnes âgées) avec des paramètres de transmission et de récupération distincts, les équations pour chaque groupe \(i\) (jeunes et personnes âgées). Ces équations différentielles sont résolues simultanément pour chaque sous-groupe, permettant de modéliser des dynamiques de diffusion différentes au sein des sous-populations.

**Interactions entre Sous-Groupes**

Pour un modèle encore plus réaliste, on peut introduire des interactions entre les sous-groupes. Par exemple, dans le cas où les jeunes interagissent avec les personnes âgées, le taux de transmission pour un groupe peut dépendre des individus infectés dans l’autre groupe.

Pour intégrer l’hétérogénéité de façon plus détaillée, on peut utiliser une **matrice de contact** \( C \) qui décrit la fréquence des contacts entre différents sous-groupes de la population. La matrice \( C \) est utilisée pour pondérer les taux de transmission entre les groupes, rendant le modèle plus flexible et capable de représenter des interactions complexes.

Dans un modèle SIR avec une matrice de contact, l’équation de la dynamique des susceptibles pour le groupe \( i \) prend la forme :

$$
\frac{dS_i}{dt} = - S_i \sum_{j} \beta_{i,j} C_{i,j} I_j
$$

où :
- \( C_{i,j} \) est le nombre moyen de contacts entre un individu du groupe \( i \) et un individu du groupe \( j \),
- \( \beta_{i,j} \) est le taux de transmission pour les contacts entre les groupes \( i \) et \( j \),
- \( I_j \) est la proportion d’infectés dans le groupe \( j \).

Ainsi, la matrice \( C \) ajuste les taux de transmission selon les fréquences de contacts entre sous-groupes, simulant des environnements sociaux où certains groupes sont plus en contact avec d’autres (par exemple, interactions intergénérationnelles).

**Exemple Numérique : Modèle SIR avec Deux Sous-Groupes**

Pour illustrer, considérons un modèle simple avec deux sous-groupes : jeunes (1) et personnes âgées (2). Supposons les paramètres suivants :

- **Taux de transmission** : \(\beta_{1,1} = 0.03\), \(\beta_{2,2} = 0.02\), \(\beta_{1,2} = 0.01\), \(\beta_{2,1} = 0.015\),
- **Taux de récupération** : \(\gamma_1 = 0.1\), \(\gamma_2 = 0.05\),
- **Contacts intergroupes** : \(C_{1,1} = 10\), \(C_{2,2} = 5\), \(C_{1,2} = 4\), \(C_{2,1} = 3\).

Les équations différentielles pour \( S_1 \), \( I_1 \), \( R_1 \) et \( S_2 \), \( I_2 \), \( R_2 \) deviennent :
$$
\frac{dS_1}{dt} = - S_1 (\beta_{1,1} C_{1,1} I_1 + \beta_{1,2} C_{1,2} I_2)
$$
$$
\frac{dI_1}{dt} = S_1 (\beta_{1,1} C_{1,1} I_1 + \beta_{1,2} C_{1,2} I_2) - \gamma_1 I_1
$$
$$
\frac{dR_1}{dt} = \gamma_1 I_1
$$
$$
\frac{dS_2}{dt} = - S_2 (\beta_{2,2} C_{2,2} I_2 + \beta_{2,1} C_{2,1} I_1)
$$
$$
\frac{dI_2}{dt} = S_2 (\beta_{2,2} C_{2,2} I_2 + \beta_{2,1} C_{2,1} I_1) - \gamma_2 I_2
$$
$$
\frac{dR_2}{dt} = \gamma_2 I_2
$$

Ces équations peuvent être résolues numériquement pour analyser l’évolution de la proportion de susceptibles, infectés et récupérés dans chaque groupe, et évaluer l'impact des interactions entre sous-groupes.

**Avantages et Limites des Modèles SIR/SIS Hétérogènes**
- **Réalisme accru** : Les modèles SIR et SIS hétérogènes offrent une représentation plus réaliste de la propagation dans des populations complexes, avec des taux d’infection variables selon les caractéristiques individuelles.
- **Flexibilité pour modéliser des interventions** : Ces modèles permettent de tester des stratégies ciblées (par exemple, vacciner en priorité les groupes les plus à risque) en ajustant les paramètres par sous-groupe.

Mais

- **Complexité mathématique accrue** : L'ajout de sous-groupes et d’interactions augmente la complexité du système d’équations différentielles et peut rendre leur résolution analytique impossible. La résolution numérique devient alors nécessaire.
- **Données nécessaires pour la matrice de contact** : Le calibrage des modèles hétérogènes exige des données empiriques détaillées sur les contacts et interactions entre sous-populations, souvent difficiles à obtenir.

En conclusion, l’ajout de l’hétérogénéité dans les modèles SIR et SIS améliore la précision des prédictions dans des contextes épidémiologiques réels et facilite l’évaluation d’interventions ciblées. Pour les infections où l'immunité acquise après guérison est temporaire, une immunité partielle ou déclinante peut être intégrée au modèle. Ce type de dynamique est pertinent pour les maladies telles que la grippe, où les individus récupérés peuvent redevenir susceptibles après une certaine période. Le modèle SIRS (Susceptible-Infected-Recovered-Susceptible) est une extension du modèle SIR, qui introduit cette perte d’immunité pour modéliser des processus épidémiologiques où la réinfection est possible.

### Modèle SIRS : Immunité temporaire

Dans le modèle SIRS, les individus passent par les mêmes trois états que dans le modèle SIR — Susceptible (\(S\)), Infecté (\(I\)), et Récupéré (\(R\)) — mais avec une différence majeure : l'état R n'est pas permanent. Après une période de récupération, les individus récupérés peuvent redevenir susceptibles.

Les équations différentielles du modèle SIRS sont les suivantes :
$$
\frac{dS}{dt} = -\beta S I + \delta R
$$
$$
\frac{dI}{dt} = \beta S I - \gamma I
$$
$$
\frac{dR}{dt} = \gamma I - \delta R
$$
où :
- \( \beta \) est le taux de transmission de l’infection (comme dans le modèle SIR),
- \( \gamma \) est le taux de récupération,
- \( \delta \) est le taux de perte d’immunité, soit le taux de passage de l’état R (Récupéré) à l’état S (Susceptible).

**Interprétation des Paramètres**

- **Taux de transmission (\(\beta\))** : Probabilité de transmission de l’infection entre une personne infectée et une personne susceptible lors d’un contact.
- **Taux de récupération (\(\gamma\))** : Taux de passage d'un individu infecté à l’état récupéré, représentatif de la durée moyenne de la période infectieuse.
- **Taux de perte d’immunité (\(\delta\))** : Paramètre crucial du modèle SIRS, il représente le taux auquel les individus récupérés perdent leur immunité et redeviennent susceptibles. Ce taux est souvent basé sur la durée moyenne de l’immunité acquise (par exemple, six mois ou un an pour certains virus).

**Dynamique des Compartiments**

1. **De S à I (infection)** : Les individus susceptibles (\(S\)) deviennent infectés (\(I\)) lorsqu’ils entrent en contact avec des infectés, avec un taux de transmission \(\beta\).
2. **De I à R (récupération)** : Les infectés (\(I\)) récupèrent après une période d’infection et deviennent temporairement immunisés, passant dans le compartiment récupéré (\(R\)), avec un taux de récupération \(\gamma\).
3. **De R à S (perte d’immunité)** : Les individus récupérés perdent leur immunité après une période donnée, avec un taux de perte d’immunité \(\delta\), et redeviennent susceptibles d’infection.

Ce modèle cyclique est pertinent pour les infections saisonnières ou récurrentes, où la réinfection est possible une fois que l’immunité diminue.

**Exemple Numérique du Modèle SIRS**

Prenons un exemple avec les paramètres suivants :
- **Taux de transmission** (\(\beta\)) : 0.3
- **Taux de récupération** (\(\gamma\)) : 0.1
- **Taux de perte d’immunité** (\(\delta\)) : 0.05

Ces paramètres indiquent que :
- En moyenne, une personne infectée transmet la maladie à 30 % de ses contacts avec des susceptibles.
- La durée moyenne de l'infection est de \(1/\gamma = 10\) jours.
- La durée moyenne d'immunité après récupération est de \(1/\delta = 20\) jours, après quoi les individus récupérés redeviennent susceptibles.

Le système d’équations différentielles devient :

\[
\frac{dS}{dt} = -0.3 S I + 0.05 R
\]
\[
\frac{dI}{dt} = 0.3 S I - 0.1 I
\]
\[
\frac{dR}{dt} = 0.1 I - 0.05 R
\]

**Analyse des Dynamiques du Modèle SIRS**

1. **Cycle de Réinfection** : Contrairement au modèle SIR, le modèle SIRS permet un retour cyclique de la maladie, car les individus récupérés peuvent redevenir susceptibles. Cela peut conduire à des cycles épidémiques récurrents, particulièrement en présence de variations saisonnières ou d’un taux de perte d’immunité élevé.

2. **Équilibre Endémique** : Dans certains cas, le modèle SIRS atteint un équilibre endémique, où la maladie persiste dans la population à un niveau stable. Ce phénomène se produit lorsque le taux de réinfection équilibre le taux de récupération, et que la fraction d'individus infectés reste constante dans le temps.

3. **Impact des Paramètres \(\delta\) et \(\beta\)** : 
   - Un **taux de perte d’immunité élevé** (\(\delta\)) conduit à un retour plus rapide des récupérés dans la catégorie des susceptibles, augmentant ainsi le risque de réinfections.
   - Un **taux de transmission élevé** (\(\beta\)) favorise des épidémies plus larges et plus fréquentes, surtout si la perte d’immunité est rapide.

**Modifications du Modèle SIRS pour Intégrer des Populations Hétérogènes**

Pour des populations hétérogènes, le modèle SIRS peut être divisé en sous-groupes (comme pour les modèles SIR et SIS hétérogènes). Par exemple, en distinguant les sous-groupes « jeunes » et « personnes âgées » avec des taux spécifiques de transmission, récupération, et perte d’immunité, les équations deviennent :

\[
\frac{dS_i}{dt} = -\beta_i S_i I_i + \delta_i R_i
\]
\[
\frac{dI_i}{dt} = \beta_i S_i I_i - \gamma_i I_i
\]
\[
\frac{dR_i}{dt} = \gamma_i I_i - \delta_i R_i
\]

Les interactions entre sous-groupes peuvent être intégrées comme suit, en utilisant une matrice de contact \(C\) qui pondère les interactions intergroupes pour chaque groupe \(i\) et \(j\) :

\[
\frac{dS_i}{dt} = -S_i \sum_j \beta_{i,j} C_{i,j} I_j + \delta_i R_i
\]
\[
\frac{dI_i}{dt} = S_i \sum_j \beta_{i,j} C_{i,j} I_j - \gamma_i I_i
\]
\[
\frac{dR_i}{dt} = \gamma_i I_i - \delta_i R_i
\]

Ici :
- \( \beta_{i,j} \) est le taux de transmission entre les groupes \(i\) et \(j\),
- \( C_{i,j} \) est la fréquence des contacts entre \(i\) et \(j\),
- \( \delta_i \) représente la perte d’immunité spécifique à chaque groupe.

**Avantages**
- **Modélisation des Réinfections** : Le modèle SIRS est adapté pour représenter les maladies récurrentes et saisonnières en permettant des réinfections.
- **Flexibilité pour les Infections Temporaires** : En ajustant \(\delta\), ce modèle s’adapte aux maladies pour lesquelles l’immunité ne dure qu’un certain temps.

mais

- **Complexité pour les Populations Hétérogènes** : Lorsqu'il est appliqué à des populations hétérogènes, le modèle SIRS devient mathématiquement plus complexe et peut nécessiter des simulations numériques.

**Conclusion et Application Pratique**

Le modèle SIRS est une version plus réaliste du modèle SIR pour les maladies à immunité temporaire. Il permet de capturer des cycles épidémiques et des réinfections, ce qui est essentiel pour la planification des interventions sanitaires dans le cas de maladies comme la grippe saisonnière ou d'autres infections respiratoires.

Les équations différentielles du modèle SIRS, avec les ajustements pour l’hétérogénéité, permettent d’étudier des dynamiques complexes et de prédire l'impact des réinfections. Les chercheurs peuvent ainsi ajuster les interventions en fonction de la durée moyenne d’immunité et des caractéristiques de la population, comme cibler les individus avec une immunité plus faible pour des campagnes de rappel vaccinal.

## 1.2 Fusion des deux parties : Modèles de Seuil, Influence et Super-Propagateurs dans la Diffusion Sociale et Épidémiologique

Les modèles de seuil et le concept de super-propagateurs sont devenus centraux pour modéliser la diffusion de comportements, d’opinions et de maladies. Ces modèles ajoutent une dimension d’influence sociale et individuelle, dépassant les cadres classiques de diffusion épidémiologique (comme les modèles SIR ou SIS) en intégrant la résistance individuelle et le rôle d’acteurs clés dans la propagation.

### Définition des Seuils d’Adoption et de l’Influence : Super-Propagateurs

Le **modèle de seuil** repose sur l'idée que chaque individu dans un réseau a un seuil personnel d’adoption, soit un nombre minimum de voisins adoptant un comportement ou une idée pour que cet individu l'adopte également. En parallèle, certains nœuds, appelés **super-propagateurs**, jouent un rôle décisif en raison de leur influence élevée (par exemple, popularité ou centralité) et de leur capacité à affecter une large partie du réseau.

- **Granovetter (1978)** pose les bases de cette théorie en expliquant que le comportement d'un individu est influencé par un seuil personnel, défini par ses liens sociaux et son contexte. 
- **Watts (2002)** formalise cette approche dans des réseaux à grande échelle, montrant comment une faible proportion de super-propagateurs peut influencer une large portion du réseau, même si la majorité des individus ont des seuils d’adoption élevés.

Les super-propagateurs sont particulièrement influents car ils ont de nombreux liens dans le réseau, ce qui augmente la probabilité que leurs comportements soient observés et adoptés par d’autres. Ce rôle des super-propagateurs est essentiel dans la diffusion d'informations, d'innovations et de maladies.

### Hétérogénéité des Seuils et Influences Pondérées

Dans les modèles de seuil avancés, on prend en compte l’hétérogénéité des individus en intégrant des seuils d’adoption variables et des influences pondérées. En effet, les individus réagissent différemment à la pression sociale, ce qui reflète la complexité des dynamiques sociales :

- **Seuil d’adoption variable** : Chaque individu \(i\) a un seuil d’adoption personnel, \(\theta_i\), qui peut varier selon des facteurs tels que l’ouverture d’esprit, la position sociale, ou le niveau de résistance. Ainsi, un individu réfractaire adoptera un comportement seulement si une forte proportion de ses voisins l’adopte également, tandis qu’un individu réceptif pourra l’adopter dès qu’il observe quelques influenceurs proches.
  
- **Influences pondérées** : Tous les liens ne sont pas égaux en influence. Un lien social fort (par exemple, un ami proche) peut avoir plus d'impact qu'un lien faible. Dans ce contexte, l'influence de chaque voisin \(j\) est pondérée par un coefficient \(w_{ij}\), représentant la force d’influence du voisin \(j\) sur \(i\).

Ces paramètres ajoutent de la précision en modélisant l’influence individuelle et la diversité des réactions face aux comportements d’adoption.

### Modélisation Mathématique : Seuils et Influences Pondérées

La condition d’adoption pour chaque individu dans un modèle de seuil hétérogène avec influences pondérées peut être formulée comme suit :

\[
\sum_{j \in \text{Voisins}(i)} w_{ij} \cdot x_j \geq \theta_i
\]

où :
- \( w_{ij} \) est le poids de l’influence du voisin \(j\) sur \(i\),
- \( x_j \) est l’état d’adoption de \(j\) (1 si \(j\) a adopté le comportement, 0 sinon),
- \( \theta_i \) est le seuil d’adoption personnel de \(i\).

Cette équation illustre que l’adoption d’un comportement par un individu dépend non seulement du nombre de voisins adoptants mais aussi de l’intensité de leurs influences respectives.

### Design de Recherche pour l’Application des Modèles de Seuil

Pour mettre en œuvre ces modèles dans une étude empirique, il est important de bien structurer le design de recherche, en définissant précisément les nœuds, les seuils d’adoption et les super-propagateurs :

1. **Identification des Nœuds et des Liens** : Chaque nœud représente un individu ou une entité, tandis que les liens représentent des relations d’influence ou de contact social. Les poids d’influence sont affectés selon la proximité relationnelle ou la centralité des nœuds dans le réseau.
   
2. **Définition des Seuils d’adoption** : Les seuils d’adoption peuvent être :
   - Fixes pour tous les nœuds (simplification),
   - Distribués aléatoirement pour représenter la diversité des sensibilités individuelles.

3. **Identification des Super-Propagateurs** : En analysant la structure du réseau, les nœuds avec une centralité élevée (nombre de liens ou capacité d’influence) sont identifiés comme super-propagateurs. Leur présence dans le modèle initiale ou en tant que premiers adoptants peut accélérer la propagation de manière significative.

### Simulation du Modèle et Interprétation des Résultats

Avec ces paramètres, le modèle de seuil avec super-propagateurs peut être simulé à travers les étapes suivantes :

1. **Initialisation** : Une fraction initiale de nœuds (par exemple, les super-propagateurs) est définie comme adoptants.
2. **Propagation itérative** : Chaque nœud évalue à chaque itération si le nombre de ses voisins ayant adopté dépasse son seuil personnel. Le modèle itère jusqu’à un état stable.
3. **Analyse des Variables** : Pour comprendre la dynamique de diffusion, on observe :
   - La vitesse de propagation,
   - La taille finale de la diffusion,
   - Le rôle des super-propagateurs.

### Analyse des Résultats : Effet des Super-Propagateurs et Sensibilité aux Seuils

Les simulations montrent des dynamiques caractéristiques liées aux super-propagateurs et aux seuils d’adoption :

1. **Impact des Super-Propagateurs** : Ces nœuds, du fait de leur connectivité élevée, peuvent provoquer une diffusion rapide et large, même lorsque les seuils d’adoption sont élevés. Les super-propagateurs jouent un rôle clé dans l’accélération et l’expansion de la propagation.

2. **Effet des Seuils** :
   - Des seuils faibles favorisent une adoption rapide, car les individus adoptent le comportement dès qu'une petite fraction de leurs voisins l'a fait.
   - Des seuils élevés rendent la propagation plus difficile, nécessitant la présence de clusters denses ou de super-propagateurs pour atteindre une diffusion significative.

3. **Impact de la Structure du Réseau** :
   - **Réseaux de petits mondes** : Facilitent une diffusion rapide grâce aux courtes distances entre nœuds.
   - **Réseaux sans échelle** : Permettent une diffusion étendue, soutenue par les super-propagateurs, et un effet d'onde où la propagation touche successivement les clusters.

### Conclusion

Les modèles de seuil et d’influence pondérée enrichissent notre compréhension de la diffusion dans les réseaux sociaux et épidémiologiques en intégrant la diversité des sensibilités individuelles et la puissance des super-propagateurs. En appliquant des seuils variables et des poids d'influence, ces modèles permettent aux chercheurs d’analyser les comportements collectifs de manière plus réaliste et de prévoir les dynamiques d’adoption dans des systèmes complexes. Les modèles avancés de propagation montrent également comment des structures de réseau, comme les réseaux de petits mondes ou sans échelle, influencent l'efficacité des super-propagateurs et la persistance de la diffusion.
## Références

Voici la bibliographie APA des études mentionnées :

- Aral, S., & Walker, D. (2012). Identifying influential and susceptible members of social networks. *Science*, 337(6092), 337-341. https://doi.org/10.1126/science.1215842

- Aral, S., Muchnik, L., & Sundararajan, A. (2009). Distinguishing influence-based contagion from homophily-driven diffusion in dynamic networks. *Proceedings of the National Academy of Sciences*, 106(51), 21544-21549. https://doi.org/10.1073/pnas.0908800106

- Bakshy, E., Hofman, J. M., Mason, W. A., & Watts, D. J. (2011). Everyone’s an influencer: Quantifying influence on Twitter. *Proceedings of the fourth ACM international conference on Web search and data mining*, 65-74. https://doi.org/10.1145/1935826.1935845

- Bakshy, E., Rosenn, I., Marlow, C., & Adamic, L. (2012). The role of social networks in information diffusion. *Proceedings of the 21st international conference on World Wide Web*, 519-528. https://doi.org/10.1145/2187836.2187907

- Berger, J., & Milkman, K. L. (2012). What makes online content viral? *Journal of Marketing Research*, 49(2), 192-205. https://doi.org/10.1509/jmr.10.0353

- Berger, J. (2013). *Contagious: How to build word of mouth in the digital age*. Simon & Schuster.

- Freeman, L. C. (1977). A set of measures of centrality based on betweenness. *Sociometry*, 40(1), 35-41. https://doi.org/10.2307/3033543

- Granovetter, M. (1978). Threshold models of collective behavior. *American Journal of Sociology*, 83(6), 1420-1443. https://doi.org/10.1086/226707

- Katz, E., & Lazarsfeld, P. F. (1955). *Personal influence: The part played by people in the flow of mass communications*. Free Press.

- Kietzmann, J. H., Hermkens, K., McCarthy, I. P., & Silvestre, B. S. (2011). Social media? Get serious! Understanding the functional building blocks of social media. *Business Horizons*, 54(3), 241-251. https://doi.org/10.1016/j.bushor.2011.01.005

- Rogers, E. M. (2003). *Diffusion of innovations* (5th ed.). Free Press.

- Valente, T. W. (1996). Social network thresholds in the diffusion of innovations. *Social Networks*, 18(1), 69-89. https://doi.org/10.1016/0378-8733(95)00256-1

- Vosoughi, S., Roy, D., & Aral, S. (2018). The spread of true and false news online. *Science*, 359(6380), 1146-1151. https://doi.org/10.1126/science.aap9559

- Watts, D. J. (2002). A simple model of global cascades on random networks. *Proceedings of the National Academy of Sciences*, 99(9), 5766-5771. https://doi.org/10.1073/pnas.082090499

- Watts, D. J., & Dodds, P. S. (2007). Influentials, networks, and public opinion formation. *Journal of Consumer Research*, 34(4), 441-458. https://doi.org/10.1086/518527

# II - Modélisation et code R d'analyse épidémiologique

### 2.1 Modèle SIR

Pour opérationnaliser chaque étape de la partie I de votre cours avec du code R, nous utiliserons principalement les packages **EpiModel** et **epidemia**. Ces packages permettent de modéliser la dynamique épidémiologique de manière flexible en s’appuyant sur les équations du modèle SIR (Susceptible-Infected-Recovered) et en intégrant des paramètres comme le taux de transmission (\(\beta\)) et le taux de guérison (\(\gamma\)). Voici comment procéder, étape par étape, pour construire et analyser le modèle en s'appuyant sur la littérature académique pour optimiser les fonctions.

Assurez-vous d’avoir les packages **EpiModel** et **epidemia** installés. 

```r
install.packages("EpiModel")
install.packages("epidemia")
library(EpiModel)
library(epidemia)
```

Pour modéliser la propagation de la participation à une controverse sur Twitter en utilisant un modèle SIR, nous considérerons les comptes Twitter comme des "individus" qui peuvent passer par trois états : **Susceptible** (n’a pas encore participé), **Infecté** (a commencé à participer), et **Récupéré** (a cessé de participer). Les paramètres clés de ce modèle sont :

- **Date d'entrée dans la controverse** : Représente le moment où un compte passe de l'état Susceptible (n’a pas encore participé) à l'état Infecté (commence à participer).
- **Date de sortie de la controverse** : Représente le moment où un compte passe de l'état Infecté à l'état Récupéré (cesse de participer).
- **Nombre de contacts durant la controverse** : Nombre d’interactions avec d'autres comptes pendant la participation à la controverse.
- **Nombre d’infectés durant la controverse** : Nombre de nouveaux comptes que ce compte a influencés ou "infectés" (incité à participer).

#### Étapes pour Construire le dataframe SIR de la Controverse

1. **Calcul du Taux de Récupération (\(\gamma\))** : Le taux auquel les comptes cessent de participer.
2. **Calcul du Taux de Transmission (\(\beta\))** : Le taux auquel les comptes infectent d'autres comptes et les incitent à participer.
3. **Simulation de la Dynamique de la Controverse** : Utilisation des paramètres \(\beta\) et \(\gamma\) pour simuler et analyser l’évolution de la controverse sur le réseau.

**Étape 1 : Calcul du Taux de Récupération (\(\gamma\))**

Le taux de récupération \(\gamma\) représente la probabilité qu'un compte infecté cesse de participer à la controverse (passe de l’état Infecté à l’état Récupéré). Pour estimer ce taux, nous pouvons utiliser la durée moyenne de participation à la controverse pour chaque compte.

1. **Durée de Participation** : Calculez la durée de participation pour chaque compte comme la différence entre la `date de sortie` et la `date d'entrée`.

   ```r
      data$duration <- as.numeric(difftime(data$date_sortie, data$date_entree, units = "days"))
   data$duration <- as.numeric(difftime(data$date_sortie, data$date_entree, units = "days"))
   ```

2. **Estimation de \(\gamma\)** : Le taux de récupération est donné par l'inverse de la durée moyenne de participation.

   ```r
   gamma <- 1 / mean(data$duration, na.rm = TRUE)
   cat("Taux de récupération (gamma) :", gamma)
   ```

La date de sortie peut être estime à partir de la dernière réaction plus 3h chez twitter/X

**Étape 2 : Calcul du Taux de Transmission (\(\beta\))**

Le taux de transmission \(\beta\) représente la probabilité qu'un compte infecté incite un compte susceptible à participer à la controverse.

1. **Calcul des Interactions Effectives** : Le nombre de contacts d'un compte infecté avec d'autres comptes est donné par la colonne `nb_contacts`. Pour obtenir le nombre de contacts susceptibles-infectés (contacts effectifs), nous utilisons le nombre total de contacts susceptibles-infectés pendant la controverse.

   ```r
   total_contacts <- sum(data$nb_contacts, na.rm = TRUE)
   ```

Le nombre de contact par tweet est en moyenne de 0.1 * de followers total
2. **Estimation de \(\beta\)** : Utilisez la proportion d'infections (nombre d’infections causées par chaque compte infecté) divisée par le nombre de contacts effectifs.

   ```r
   # Nombre total de nouveaux infectés causés par tous les comptes infectés
   total_infections <- sum(data$nb_infectes, na.rm = TRUE)
   
   # Calcul de beta
   beta <- total_infections / total_contacts
   cat("Taux de transmission (beta) :", beta)

   ```

L'act.rate dans tweeter et le nb.de contact/3 (durée d'exposition moyen)
#### Initialisation des Paramètres du Modèle SIR avec **EpiModel**

**EpiModel** est un package de référence pour la simulation des modèles épidémiologiques basés sur des équations différentielles. Nous allons paramétrer le modèle SIR en spécifiant la taille de la population, les taux de transmission et de guérison, et les conditions initiales.

1. **Définition des Paramètres**

Selon Kermack et McKendrick (1927), les paramètres \(\beta\) (taux de transmission) et \(\gamma\) (taux de guérison) déterminent la vitesse de propagation de l’infection. Le nombre de reproduction de base (\(R_0\)) est défini comme \(\frac{\beta}{\gamma}\).

   ```r
   # Paramètres du modèle
   param <- param.dcm(inf.prob = 0.3, act.rate = 0.5, rec.rate = 0.1)
   ```

   - `inf.prob` représente \(\beta\), soit la probabilité de transmission de l’infection à chaque interaction.
   - `act.rate` est le taux d’activité (nombre de contacts susceptibles de transmettre l’infection).
   - `rec.rate` représente \(\gamma\), soit le taux de guérison ou de passage à l’état R.

2. **Définition des Conditions Initiales**

Initialisez la population avec un grand nombre d’individus susceptibles, quelques infectés, et aucun récupéré.

   ```r
   # Conditions initiales : nombre de personnes dans chaque compartiment
   init <- init.dcm(s.num = 999, i.num = 1, r.num = 0)
   ```

3. **Définition du Contrôle du Modèle**

Spécifiez le type de modèle et le nombre d’étapes temporelles de la simulation.

   ```r
   # Contrôle de la simulation
   control <- control.dcm(type = "SIR", nsteps = 100, dt = 1)
   ```

4. **Exécution du Modèle et Visualisation des Résultats**

Avec ces paramètres, exécutez le modèle et visualisez les résultats pour observer l’évolution des compartiments S, I, et R.

```r
# Exécution de la simulation
model_sir <- dcm(param, init, control)

# Visualisation des résultats
plot(model_sir)
```

Ce graphique montre l’évolution de la proportion d’individus dans chaque compartiment (susceptibles, infectés, récupérés) au fil du temps.

5. **Calcul du Nombre de Reproduction de Base \( R_0 \)**

Le nombre de reproduction de base \(R_0\) est calculé comme le rapport \(\frac{\beta}{\gamma}\), et il sert à évaluer si l’infection peut se propager dans la population.

```r
# Calcul du nombre de reproduction de base
R0 <- param$inf.prob / param$rec.rate
cat("Le nombre de reproduction de base (R0) est de :", R0)
```

Si \( R_0 > 1 \), l’infection est susceptible de se propager dans la population, comme indiqué dans la littérature par Kermack et McKendrick (1927) et confirmé par des travaux récents sur la dynamique des épidémies (Anderson et May, 1991).

Oui, **EpiModel** gère les modèles avec des **sous-groupes**. Cela permet de diviser la population en différents groupes ou catégories pour mieux représenter l'hétérogénéité dans la transmission et la récupération. Les sous-groupes peuvent être définis en fonction de caractéristiques démographiques (âge, sexe), de comportements spécifiques (comme le nombre moyen de contacts), ou d'autres facteurs pertinents pour la dynamique de la propagation.

#### Fonctionnement des Sous-groupes dans EpiModel

EpiModel permet d'intégrer des sous-groupes dans les modèles SIR, SIS, et autres modèles épidémiologiques à travers des paramètres spécifiques. Voici quelques éléments clés :

1. **Définition des Sous-groupes** : Lors de la configuration des paramètres initiaux (par exemple avec `param.dcm`), vous pouvez spécifier les tailles de différents sous-groupes et ajuster les paramètres de transmission (`inf.prob`), de récupération (`rec.rate`), et de contact (`act.rate`) pour chaque groupe.

2. **Utilisation des Sous-groupes** : Les sous-groupes peuvent être utilisés pour modéliser des populations qui interagissent différemment :
   - Par exemple, on pourrait avoir un sous-groupe avec des superpropagateur et des twettos normaux.
   - Les taux de transmission et de récupération peuvent aussi varier selon les sous-groupes, permettant de simuler des dynamiques épidémiologiques réalistes.

3. **Paramétrage des Modèles en Sous-groupes** : Les paramètres des sous-groupes sont définis sous forme de vecteurs, avec chaque élément correspondant à un sous-groupe. Par exemple :
   
   ```r
   library(EpiModel)
   
   # Paramètres avec deux sous-groupes
   param <- param.dcm(inf.prob = c(0.3, 0.1), act.rate = c(0.5, 0.2), rec.rate = c(0.1, 0.05))
   init <- init.dcm(s.num = c(500, 500), i.num = c(10, 5), r.num = c(0, 0))
   control <- control.dcm(type = "SIR", nsteps = 100)
   
   # Modèle avec sous-groupes
   model <- dcm(param, init, control)
   plot(model)
   ```

Dans cet exemple, la population est divisée en deux sous-groupes avec des taux de transmission (`inf.prob`), de contact (`act.rate`), et de récupération (`rec.rate`) différents.

**Applications des Sous-groupes**

Les sous-groupes dans **EpiModel** permettent de :

- **Modéliser des populations hétérogènes** : Comme les populations d'âges différents ou avec des comportements différents.
- **Étudier les effets de politiques ciblées** : Par exemple, en analysant l’impact de la vaccination d’un sous-groupe à haut risque.
- **Améliorer la précision des simulations** : En représentant des structures de contact plus réalistes, comme dans les réseaux sociaux ou les groupes à risque.

En résumé, **EpiModel** offre une flexibilité importante pour créer des modèles épidémiologiques multi-groupes et pour analyser la dynamique de propagation dans des populations hétérogènes.


#### Références Académiques Utilisées pour la Construction des Fonctions

- **Kermack, W. O., & McKendrick, A. G. (1927).** A contribution to the mathematical theory of epidemics. *Proceedings of the Royal Society of London. Series A, Containing Papers of a Mathematical and Physical Character*, 115(772), 700-721. https://doi.org/10.1098/rspa.1927.0118

- **Anderson, R. M., & May, R. M. (1991).** *Infectious diseases of humans: Dynamics and control*. Oxford University Press.

Ces travaux offrent les bases théoriques pour les paramètres \(\beta\) et \(\gamma\), ainsi que pour le calcul de \(R_0\), et leurs résultats ont été implémentés ici dans une approche pratique pour le calcul et la visualisation en R.

### 2.2 Simulation épidémique en réseaux : effet de seuil et super propagateur

Dans **EpiModel**, il est possible de créer une simulation de propagation sur un réseau où chaque nœud (individu) possède une caractéristique d'influence (capacité à transmettre ou influencer) et une caractéristique de résistance (susceptibilité à l’influence ou infection). Pour cela, on peut utiliser des attributs de nœuds pour représenter ces caractéristiques et moduler les probabilités de transmission et d'adoption en fonction de ces attributs.

#### Étape 1 : Un réseau initialement infecté

1. **Démarrer la simulation avec des états initiaux spécifiques** (infecté/susceptible) pour chaque nœud du réseau, définis directement dans le réseau de base.
2. **Simuler plusieurs scénarios de départ de contagion**, en ajustant les nœuds infectés initiaux dans différents scénarios de simulation.

**Démarrer la Simulation avec un État Initial Spécifique (1/0)**

Chaque noeud à une variable (de préférence 0 à 1) influence et resistance.

Pour initialiser la simulation avec des états infectés (1) ou susceptibles (0) directement dans le réseau, vous pouvez définir l’état initial (`inf.status`) pour chaque nœud dans le réseau de base. **EpiModel** utilisera ensuite ces valeurs pour commencer la simulation avec les nœuds spécifiés comme infectés.

#### **Étape 2 : Paramétrer la Probabilité de Transmission en Fonction des Attributs**

Dans **EpiModel**, on peut utiliser des **règles personnalisées** pour ajuster la probabilité de transmission en fonction des attributs des nœuds. Voici comment adapter la probabilité de transmission pour que les nœuds avec des valeurs d’influence plus élevées aient un taux de transmission plus fort et que les nœuds plus résistants aient une probabilité plus faible d’être infectés.

1. **Paramétrer la Fonction de Transmission Personnalisée** :
   - La fonction de transmission personnalisée utilise les attributs d’influence et de résistance pour déterminer la probabilité de transmission pour chaque lien.
   - Par exemple, la probabilité de transmission entre deux nœuds pourrait être ajustée selon la formule :
     \[
     \text{probabilité\ de\ transmission} = \beta \times \text{influence du nœud infecté} / \text{résistance du nœud susceptible}
     \]

2. **Définir la Fonction de Probabilité de Transmission** :
   - Utilisez un modèle de contrôle stochastique personnalisé avec cette logique.

```r
# Fonction de transmission
transmission_function <- function(dat, at) {
  # Obtenir les indices des nœuds infectés et susceptibles
  active <- which(dat$attr$inf.status == 1) # nœuds infectés
  susceptible <- which(dat$attr$inf.status == 0) # nœuds susceptibles
  
  # Parcourir chaque nœud infecté et tenter de transmettre l'infection
  for (i in active) {
    # Obtenir les voisins susceptibles
    neighbors <- get.neighborhood(dat$nw, i)
    neighbors <- neighbors[dat$attr$inf.status[neighbors] == 0] # filtrer pour ne garder que les susceptibles
    
    # Calcul de la transmission ajustée pour chaque voisin
    for (j in neighbors) {
      influence_i <- dat$attr$influence[i]
      resistance_j <- dat$attr$resistance[j]
      
      # Calcul de la probabilité de transmission ajustée
      prob_transmit <- dat$param$base_transmit * (influence_i / resistance_j)
      
      # Transmission avec probabilité ajustée
      if (runif(1) < prob_transmit) {
        dat$attr$inf.status[j] <- 1 # Le voisin j devient infecté
      }
    }
  }
  return(dat)
}
```

#### **Étape 3 : Lancer la Simulation**

**Configurer le Contrôle pour Appeler la Fonction de Transmission Personnalisée** :
   - Le contrôle du modèle doit être configuré pour utiliser la fonction `transmission_function`.

```r
# Paramètres de transmission et récupération
param <- param.net(base_transmit = 0.1, rec.rate = 0.05)

# Les conditions initiales sont basées sur l'attribut "inf.status"
init <- init.net(i.num = 0)  # Ne pas spécifier ici car nous avons défini manuellement dans `inf.status`

# Contrôle de la simulation avec fonction de transmission personnalisée
control <- control.net(type = "SIS", nsteps = 100, infection.FUN = transmission_function)

# Exécution de la simulation
sim <- netsim(network, param, init, control)
```

3. **Visualisation et Analyse des Résultats** :
   - Une fois la simulation exécutée, vous pouvez visualiser les résultats pour observer comment l’influence et la résistance affectent la dynamique de l’épidémie dans le réseau.

```r
# Résultats et visualisation
plot(sim)
```

#### Etapes 4 - Simuler Plusieurs Scénarios de Départ de Contagion

Pour simuler plusieurs scénarios de départ, vous pouvez configurer différents ensembles de nœuds initialement infectés. Cela permet d'étudier comment le choix des nœuds infectés initiaux influence la propagation dans le réseau, en testant par exemple l'impact de différents super-propagateurs.

Voici comment configurer des scénarios multiples :

1. **Définir plusieurs configurations d’états initiaux** :
   - Par exemple, vous pourriez définir une liste de vecteurs, où chaque vecteur représente un scénario avec des nœuds initiaux infectés spécifiques.

2. **Boucle sur chaque scénario** : Lancer la simulation avec chaque configuration d’état initial, en stockant les résultats pour comparaison.

```r
# Exemples de scénarios de départ basés sur des conditions avec `which`
scenarios <- list(
  which(get.vertex.attribute(network, "influence") > 0.8),  # Scénario 1 : nœuds avec influence > 0.8
  which(get.vertex.attribute(network, "influence") < 0.2),  # Scénario 2 : nœuds avec influence < 0.2
  which(get.vertex.attribute(network, "resistance") < 0.3)  # Scénario 3 : nœuds avec faible résistance
)


# Boucle sur chaque scénario de départ
results <- list()
for (i in 1:length(scenarios)) {
  # Définir l'état initial pour le scénario courant
  initial_status <- rep(0, num_nodes)
  initial_status[scenarios[[i]]] <- 1  # Définir les nœuds infectés pour ce scénario

  # Assigner cet état initial au réseau
  set.vertex.attribute(network, "inf.status", initial_status)
  
  # Initialiser sans infectés supplémentaires
  init <- init.net(i.num = 0)
  
  # Lancer la simulation pour ce scénario
  sim <- netsim(network, param, init, control)
  
  # Sauvegarder les résultats pour comparaison
  results[[i]] <- sim
}

# Visualiser les résultats de chaque scénario pour comparaison
par(mfrow = c(2, 2))
for (i in 1:length(results)) {
  plot(results[[i]], main = paste("Scénario", i))
}
```

**Interprétation et Comparaison des Scénarios**

En configurant plusieurs scénarios de départ, vous pouvez observer :

- **La rapidité de la propagation** en fonction des nœuds initiaux infectés : certains nœuds peuvent jouer le rôle de super-propagateurs, entraînant une propagation plus rapide.
- **L’ampleur totale de la diffusion** : certains choix initiaux peuvent atteindre une plus grande partie du réseau, selon la centralité et l’interconnectivité des nœuds infectés.
- **L'effet de la position des nœuds initiaux dans la structure du réseau** : infecter des nœuds situés en périphérie du réseau peut ralentir la propagation par rapport à des nœuds centraux.

Ces simulations permettent d'analyser différents scénarios de diffusion dans un réseau, tout en prenant en compte les rôles spécifiques des nœuds en fonction de leurs caractéristiques d’influence et de résistance.


#### **Conclusion**

Cette configuration permet de simuler une épidémie où chaque nœud a des caractéristiques d’influence et de résistance, qui ajustent dynamiquement la probabilité de transmission en fonction des attributs individuels. Ce type de modèle est particulièrement utile pour étudier la propagation dans des réseaux hétérogènes, où certaines entités (super-propagateurs) jouent un rôle central dans la diffusion, tandis que d’autres sont plus résistantes à l'influence ou à l'infection. Cela crée une simulation plus réaliste, où la variabilité des comportements individuels et des interactions sociales est prise en compte, permettant d’explorer des scénarios plus proches des dynamiques épidémiologiques et sociales réelles.

III - Application du modèle SIR en sciences sociales
Bien sûr, voici un état des lieux pour trois applications des modèles SIR, de seuil, et de super-propagateurs en sciences sociales, illustré par des études de cas et des recherches de terrain qui utilisent un design de recherche structuré, des méthodes rigoureuses, et des hypothèses claires. 

# III - Application des modèles épidémiologiques au Sciences Sociales

### 1. Adoption de Nouveaux Comportements ou Objets : Étude de l'Adoption des Véhicules Électriques

**Étude :** _"The Spread of Behavior in an Online Social Network Experiment"_ par Damon Centola (2010)

- **Contexte :** Cette étude examine comment les structures de réseaux influencent la diffusion de nouveaux comportements en ligne.
    
- **Méthodologie :** Centola a mené une expérience en ligne avec plus de 1 500 participants, répartis aléatoirement dans des réseaux structurés différemment (réseaux aléatoires vs. réseaux en clusters). Les participants étaient encouragés à adopter un comportement de santé en ligne.
    
- **Résultats :** Les résultats ont montré que les réseaux en clusters facilitaient une diffusion plus rapide et plus large du comportement, soulignant l'importance des structures de réseau et des seuils d'adoption dans la propagation des comportements.
    

> [!NOTE]
> **Référence :** Centola, D. (2010). The Spread of Behavior in an Online Social Network Experiment. _Science_, 329(5996), 1194-1197.[voir](https://repository.upenn.edu/bitstreams/0fcdc75a-f702-4e68-9f58-0dd55a9e2c3c/download)

**Étude de Cas** : *L'adoption des véhicules électriques dans des communautés urbaines et rurales*

- **Contexte et Objectif de l'Étude** : Une étude menée par **Axsen et Kurani (2012)** examine l'adoption des véhicules électriques (VE) dans des communautés urbaines et rurales aux États-Unis et cherche à comprendre comment les dynamiques de seuil et les super-propagateurs influencent les décisions d’achat. En effet, l’adoption des VE est un changement de comportement majeur, influencé par des normes sociales, des interactions entre consommateurs, et des campagnes de sensibilisation.

- **Hypothèses et Modèle Théorique** : Les chercheurs hypothèsent que des super-propagateurs (ou "leaders d’opinion" comme des personnalités respectées au sein de la communauté) influencent fortement l'adoption des VE, et que les individus adoptent un comportement favorable aux VE lorsque suffisamment de leurs pairs l’ont déjà fait (effet de seuil). Ils utilisent un modèle de seuil pour estimer le point critique d’adoption.

- **Méthodologie et Design de Recherche** : Cette étude suit une approche mixte, combinant des analyses de réseaux sociaux dans différentes communautés avec des entretiens pour évaluer les seuils d’adoption des VE. Le réseau social est construit en reliant les répondants en fonction de leurs interactions et de leurs sources d’information sur les VE. La population est segmentée en groupes d'âge, revenus, et sensibilisation écologique.

- **Résultats et Observations** : Les résultats montrent que dans les communautés urbaines, où les interactions sociales sont nombreuses, l'effet des super-propagateurs est plus prononcé, et un seuil relativement bas de 10 % d’adoption est suffisant pour que les VE soient acceptés par la majorité. En revanche, dans les communautés rurales, les seuils sont plus élevés et les super-propagateurs jouent un rôle encore plus crucial en raison de la plus faible connectivité sociale. Cette étude met en évidence l’importance des super-propagateurs et des seuils d’adoption dans la diffusion de comportements pro-environnementaux.

> [!NOTE]
> Axsen, J., & Kurani, K. S. (2012a). Interpersonal Influence within Car Buyers’ Social Networks : Applying Five Perspectives to Plug-in Hybrid Vehicle Drivers. _Environment and Planning A: Economy and Space_, _44_(5), 1047‑1065. [voir](https://doi.org/10.1068/a43221x)
> 
> Axsen, J., & Kurani, K. S. (2012b). _Social Influence, Consumer Behavior, and Low-Carbon Energy Transitions_ (SSRN Scholarly Paper No. 2163621). Social Science Research Network. [voir](https://doi.org/10.1146/annurev-environ-062111-145049)

---

### 2. Controverses Politiques en Ligne : Diffusion des Idées Pendant les Élections

**Étude :** _"The Spread of True and False News Online"_ par Soroush Vosoughi, Deb Roy et Sinan Aral (2018)

- **Contexte :** Cette recherche analyse la diffusion des informations véridiques et fausses sur les réseaux sociaux, en particulier Twitter, et examine le rôle des super-propagateurs dans la propagation des controverses politiques en ligne.
    
- **Méthodologie :** Les auteurs ont analysé environ 126 000 cascades de diffusion de nouvelles, tweetées par 3 millions de personnes entre 2006 et 2017, en identifiant les caractéristiques des utilisateurs et des contenus qui influencent la propagation.
    
- **Résultats :** L'étude a révélé que les fausses nouvelles se propagent plus rapidement et plus largement que les vraies, souvent en raison de l'action de super-propagateurs qui amplifient la diffusion.
    

**Référence :** Vosoughi, S., Roy, D., & Aral, S. (2018). The Spread of True and False News Online. _Science_, 359(6380), 1146-1151.[Voir](https://www.jstor.org/stable/26401644)

**Étude de Cas** : *Diffusion des controverses politiques sur Twitter durant l’élection présidentielle américaine de 2020*

- **Contexte et Objectif de l'Étude** : **Bail et al. (2020)** ont mené une étude pour comprendre comment les idées et controverses politiques se propagent sur les réseaux sociaux, en analysant particulièrement le rôle des super-propagateurs et les seuils d'adoption. Cette étude visait à identifier si certains comptes, en raison de leur influence, pouvaient déclencher des vagues de discussions polarisées.

- **Hypothèses et Modèle Théorique** : L’hypothèse principale était que certains comptes (personnalités politiques, influenceurs, bots) agissent comme des super-propagateurs et provoquent des "vagues" de controverses dans le réseau. L’étude suppose également que l'adoption d'une opinion politique dépend de seuils d’influence, où les individus prennent part au débat lorsque plusieurs de leurs contacts y participent.

- **Méthodologie et Design de Recherche** : Les chercheurs ont collecté des données Twitter sur les interactions de 2 000 comptes à fort impact, en identifiant les retweets, mentions et réponses entre utilisateurs. Un modèle SIR modifié a été utilisé pour analyser la diffusion des messages, où les utilisateurs passent d’un état de "non-engagement" à un état "engagé" (partage d’un message controversé) et ensuite à un état "désengagé" (cesse de partager). Le modèle de seuil est appliqué pour évaluer à quel point l'adoption des opinions dépend des contacts.

- **Résultats et Observations** : Les résultats montrent que les super-propagateurs, notamment des figures politiques et des influenceurs en ligne, ont un effet disproportionné sur la diffusion. Les comptes avec des opinions polarisées, notamment, avaient un effet amplifié, entraînant des vagues de participation en cascade, même avec des seuils d’adoption élevés (plus de 20 %). Les super-propagateurs ont généré des vagues successives de discussions, même plusieurs jours après la publication initiale, et les seuils critiques variaient selon les sujets de controverses.

> [!NOTE]
> Bail, C. A., Argyle, L. P., Brown, T. W., Bumpus, J. P., Chen, H., Hunzaker, M. B. F., Lee, J., Mann, M., Merhout, F., & Volfovsky, A. (2018). Exposure to opposing views on social media can increase political polarization. _Proceedings of the National Academy of Sciences_, _115_(37), 9216‑9221. [Voir](https://www.pnas.org/doi/10.1073/pnas.1804840115)

### 3. Réseaux de Citations Académiques : Diffusion des Idées Théoriques

**Étude :** Caroline S. Wagner et Loet Leydesdorff (2009)

- **Contexte :** Cette étude explore les réseaux de co-auteurs dans la littérature scientifique, mettant en lumière les dynamiques de collaboration internationale et le rôle des super-propagateurs dans la diffusion des connaissances.
    
- **Méthodologie :** Les auteurs ont analysé les réseaux de co-auteurs à partir de bases de données bibliométriques, en identifiant les chercheurs ayant un rôle central (super-propagateurs) et en examinant les structures de réseau influençant la diffusion des idées.
    
- **Résultats :** L'étude a montré que les chercheurs occupant des positions centrales dans les réseaux de co-auteurs jouent un rôle crucial dans la diffusion des connaissances, agissant comme des super-propagateurs qui facilitent l'adoption de nouvelles idées et méthodes.
    

> [!NOTE]
> **Référence :** 
> Leydesdorff, L., & Wagner, C. (2009). _International Collaboration in Science and the Formation of a Core Group_ (No. arXiv:0911.1438). arXiv. [Voir](https://doi.org/10.48550/arXiv.0911.1438)
> 


### Synthèse

Ces études de cas montrent comment les modèles SIR, de seuil, et de super-propagateurs permettent de modéliser la diffusion dans des contextes variés :
- L’adoption de véhicules électriques dépend de la dynamique des interactions sociales et des influenceurs dans les communautés.
- Les controverses politiques en ligne sont alimentées par les super-propagateurs, qui modifient les seuils d’adoption et amplifient les débats.
- Dans les réseaux de citations académiques, les articles influents jouent un rôle de super-propagateurs, facilitant l'adoption de nouveaux concepts.

Ces modèles offrent ainsi des cadres analytiques robustes pour comprendre et anticiper les dynamiques de diffusion dans les réseaux sociaux, politiques, et académiques.
