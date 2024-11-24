# YAML de Tête

L'en-tête YAML d'un document R Markdown (`.Rmd`) permet de définir des métadonnées et des paramètres globaux influençant le rendu du document. Outre les options couramment utilisées que vous avez mentionnées, voici une liste plus exhaustive des options disponibles :

**Options générales :**

- `subtitle` : Sous-titre du document.
- `abstract` : Résumé ou description du document.
- `keywords` : Mots-clés associés au document.
- `lang` : Langue du document (par exemple, `fr` pour le français).
- `fontsize` : Taille de la police (par exemple, `11pt`, `12pt`).
- `geometry` : Paramètres de mise en page pour les documents PDF (par exemple, `margin=1in`). Le package `geometry` offre une variété de paramètres pour personnaliser la mise en page. Voici quelques-uns des plus couramment utilisés :
	- `margin` : Définit une marge uniforme sur tous les côtés.
	- `top`, `bottom`, `left`, `right` : Spécifient les marges individuelles pour chaque côté.
	- `paperwidth` et `paperheight` : Définissent les dimensions du papier.
	- `textwidth` et `textheight` : Spécifient les dimensions de la zone de texte.
	- `heightrounded` : Ajuste la hauteur du texte pour éviter les débordements de lignes.
	- `includehead` et `includefoot` : Incluent les en-têtes et pieds de page dans les calculs de mise en page.
	- `showframe` : Affiche les cadres des marges pour faciliter le réglage.
	- **Remarques importantes :**
		- Les unités de mesure couramment utilisées incluent le centimètre (`cm`), le millimètre (`mm`), le pouce (`in`) et le point typographique (`pt`).
		- Il est essentiel de s'assurer que les paramètres spécifiés sont compatibles avec le moteur LaTeX utilisé (par exemple, `pdflatex`, `xelatex`, `lualatex`).
		- Une mauvaise configuration des marges peut entraîner des problèmes de mise en page ou des avertissements lors de la compilation du document.
- `documentclass` : Classe de document LaTeX utilisée pour les documents PDF (par exemple, `article`, `report`).
	---
	title: "Titre du Document"
	author: "Nom de l'Auteur"
	output:
	  pdf_document:
	    documentclass: book
	---
	**Principales classes de document LaTeX :**
	- `article` : Utilisée pour des articles, des rapports courts ou des documents sans division en chapitres.
	- `report` : Adaptée aux documents plus longs, tels que les rapports techniques ou les mémoires, incluant des chapitres.
	- `book` : Conçue pour les livres, avec une structure complexe comprenant des parties, des chapitres et des sections.
	- `letter` : Destinée à la rédaction de lettres.
	- `beamer` : Utilisée pour créer des présentations sous forme de diapositives.
- `classoption` : Options supplémentaires pour la classe de document LaTeX.
- `header-includes` : Inclusion de commandes LaTeX ou HTML supplémentaires dans l'en-tête du document.
- `footer-includes` : Inclusion de commandes LaTeX ou HTML supplémentaires dans le pied de page du document.
- `includes` : Permet d'inclure des fichiers externes dans le document, avec les sous-options :
    - `in_header` : Fichier à inclure dans l'en-tête.
    - `before_body` : Fichier à inclure avant le corps du document.
    - `after_body` : Fichier à inclure après le corps du document.
- `link-citations` : Active les liens hypertextes pour les citations (`true` ou `false`).
- `citation_package` : Spécifie le package LaTeX à utiliser pour les citations (par exemple, `natbib`, `biblatex`).
- `biblio-style` : Style bibliographique à utiliser avec `biblatex`.
- `lot` : Inclusion de la liste des tableaux (`true` ou `false`).
- `lof` : Inclusion de la liste des figures (`true` ou `false`).
- `appendix` : Sections à inclure en annexe.
- `titlepage` : Génération d'une page de titre distincte (`true` ou `false`).
- `titlepage-color` : Couleur de fond de la page de titre (par exemple, `blue`, `#0000FF`).
- `titlepage-text-color` : Couleur du texte sur la page de titre.
- `titlepage-rule-color` : Couleur de la ligne sous le titre sur la page de titre.
- `titlepage-rule-height` : Épaisseur de la ligne sous le titre sur la page de titre.
- `mainfont` : Police principale du document.
- `sansfont` : Police sans empattement du document.
- `monofont` : Police à chasse fixe du document.
- `fontsize` : Taille de la police (par exemple, `12pt`).
- `linestretch` : Interligne du document.
- `papersize` : Taille du papier (par exemple, `a4`, `letter`).
- `geometry` : Marges et autres paramètres de mise en page (par exemple, `margin=1in`).
- `documentclass` : Classe de document LaTeX (par exemple, `article`, `report`).
- `classoption` : Options supplémentaires pour la classe de document.
- `header-includes` : Inclusion de commandes LaTeX supplémentaires dans l'en-tête.
- `output` : Permet de spécifier plusieurs formats de sortie avec des options spécifiques pour chacun.

**Options spécifiques aux formats de sortie :**

_Pour `html_document` :_

- `self_contained` : Génère un document autonome en intégrant toutes les ressources (`true` ou `false`).
- `mathjax` : Spécifie la version ou le chemin vers MathJax pour le rendu des équations.
- `css` : Chemin vers un fichier CSS personnalisé.
- `includes` : Inclusion de fichiers HTML supplémentaires avec les sous-options :
    - `in_header` : Fichier à inclure dans l'en-tête.
    - `before_body` : Fichier à inclure avant le corps du document.
    - `after_body` : Fichier à inclure après le corps du document.
- `keep_md` : Conserve le fichier Markdown intermédiaire généré (`true` ou `false`).
- `lib_dir` : Répertoire où stocker les bibliothèques externes.
- `pandoc_args` : Arguments supplémentaires à passer à Pandoc.
- `extra_dependencies` : Packages LaTeX supplémentaires à inclure.
- `highlight` : Schéma de coloration syntaxique pour le code (par exemple, `tango`, `pygments`).
- `theme` : Thème visuel pour les documents HTML (par exemple, `default`, `cerulean`, `journal`).
- `toc_float` : Rend la table des matières flottante (`true` ou `false`).
- `code_folding` : Permet de plier/déplier le code (`none`, `hide`, `show`).
- `code_download` : Ajoute un bouton pour télécharger le code source (`true` ou `false`).

**Options spécifiques aux formats de sortie :**

_Pour `pdf_document` :_

- `keep_tex` : Conserve le fichier `.tex` intermédiaire généré (`true` ou `false`).
- `latex_engine` : Moteur LaTeX à utiliser (`pdflatex`, `xelatex`, `lualatex`, `tectonic`).
- `citation_package` : Package LaTeX pour la gestion des citations (`natbib`, `biblatex`).
- `includes` : Inclusion de fichiers LaTeX supplémentaires avec les sous-options :
    - `in_header` : Fichier à inclure dans l'en-tête.
    - `before_body` : Fichier à inclure avant le corps du document.
    - `after_body` : Fichier à inclure après le corps du document.
- `fig_crop` : Recadre automatiquement les figures (`true` ou `false`).
- `toc` : Inclusion d'une table des matières (`true` ou `false`).
- `toc_depth` : Niveau de profondeur de la table des matières.
- `number_sections` : Numérotation automatique des sections (`true` ou `false`).
- `highlight` : Schéma de coloration syntaxique pour le code (par exemple, `tango`, `pygments`).
- `keep_md` : Conserve le fichier Markdown intermédiaire généré (`true` ou `false`).
- `pandoc_args` : Arguments supplémentaires à passer à Pandoc.

_Pour `word_document` :_

- `reference_docx` : Modèle Word personnalisé à utiliser pour le formatage.
- `includes` : Inclusion de fichiers supplémentaires avec les sous-options :
    - `in_header` : Fichier à inclure dans l'en-tête.
    - `before_body` : Fichier à inclure avant le corps du document.
    - `after_body` : Fichier à inclure après le corps du document.
- `toc` : Inclusion d'une table des matières (`true` ou `false`).
- `toc_depth` : Niveau de profondeur de la table des matières.
- `number_sections` : Numérotation automatique des sections (`true` ou `false`).
- `highlight` : Schéma de coloration syntaxique pour le code (par exemple, `tango`, `pygments`).
- `keep_md` : Conserve le fichier Markdown intermédiaire généré (`true` ou `false`).
- `pandoc_args` : Arguments supplémentaires à passer à Pandoc.

**Options avancées :**

- `params` : Définition de paramètres pour les rapports paramétrés. Chaque paramètre peut avoir un nom, une valeur par défaut et une description.
- `runtime` : Spécifie le mode d'exécution du document (`static`, `shiny`, `shinyrmd`).
- `output` : Permet de spécifier plusieurs formats de sortie avec des options spécifiques pour chacun.
- `knit` : Spécifie une fonction personnalisée pour le tricotage du document.
- `clean` : Indique si les fichiers intermédiaires doivent être supprimés après le tricotage (`true` ou `false`).
- `output_dir` : Répertoire de sortie pour les fichiers générés.
- `output_file` : Nom du fichier de sortie généré.
- `intermediates_dir` : Répertoire pour les fichiers intermédiaires générés lors du tricotage.
- `knit_root_dir` : Répertoire racine à utiliser lors du tricotage du document.
- `resource_files` : Liste de fichiers de ressources à inclure dans le document (par exemple, images, scripts).
- `always_allow_html` : Permet l'inclusion de contenu HTML dans les documents non-HTML (`true` ou `false`).
- `df_print` : Méthode d'impression des data frames (`default`, `kable`, `tibble`, `paged`).
- `bookdown` : Options spécifiques pour les projets utilisant le package `bookdown`.

Il est important de noter que certaines options peuvent ne pas être compatibles entre différents formats de sortie. Par conséquent, il est recommandé de consulter la documentation officielle de R Markdown et de `knitr` pour obtenir des informations détaillées sur chaque option et son utilisation appropriée.

Pour une liste complète et à jour des options disponibles, vous pouvez consulter les ressources suivantes :

- "R Markdown: The Definitive Guide" par Yihui Xie, J.J. Allaire et Garrett Grolemund.
- La documentation officielle de `rmarkdown` sur le site de RStudio.
- Les pages d'aide des fonctions `rmarkdown::html_document()`, `rmarkdown::pdf_document()` et `rmarkdown::word_document()`.

Ces ressources fournissent des informations détaillées et des exemples d'utilisation pour chaque option, facilitant ainsi la personnalisation et l'optimisation de vos documents R Markdown.

# En-tête r

Dans l'utilisation de `knitr` pour la génération de documents dynamiques avec R Markdown, certaines options de chunk sont fréquemment employées en raison de leur impact significatif sur le rendu et le contrôle du document final. Selon le principe de Pareto, environ 20 % des options sont utilisées dans 80 % des cas. Voici une liste des options les plus couramment utilisées, accompagnées de leur définition et de leur usage :

- **`eval`** : Contrôle l'évaluation du code dans le chunk. Définir `eval = FALSE` permet de désactiver l'exécution du code, utile pour afficher du code sans l'exécuter.
    
- **`echo`** : Détermine si le code source est affiché dans le document final. `echo = FALSE` masque le code tout en affichant les résultats, ce qui est pertinent pour présenter uniquement les sorties sans le code associé.
    
- **`include`** : Indique si le chunk doit être inclus dans le document final. `include = FALSE` exécute le code sans afficher ni le code ni les résultats, souvent utilisé pour des configurations ou des chargements de packages en arrière-plan.
    
- **`message`** : Contrôle l'affichage des messages générés par le code. `message = FALSE` masque les messages, ce qui est utile pour éviter l'affichage de messages non pertinents dans le document final.
    
- **`warning`** : Gère l'affichage des avertissements produits par le code. `warning = FALSE` supprime les avertissements du rendu final, permettant de maintenir un document propre.
    
- **`error`** : Détermine si les erreurs générées par le code doivent être affichées. `error = TRUE` affiche les erreurs sans interrompre la compilation, facilitant le débogage tout en poursuivant la génération du document.
    
- **`fig.width`** et **`fig.height`** : Spécifient respectivement la largeur et la hauteur des figures générées, en pouces. Ces options permettent de contrôler la taille des graphiques pour une meilleure intégration dans le document.
    
- **`fig.cap`** : Fournit une légende pour les figures, essentielle pour contextualiser les graphiques et améliorer la compréhension du lecteur.
    
- **`cache`** : Si défini sur `TRUE`, met en cache les résultats du chunk pour éviter une réévaluation lors des compilations ultérieures, accélérant ainsi le processus de génération du document.
    
- **`fig.align`** : Spécifie l'alignement des figures dans le document. Les options incluent `'left'`, `'right'` et `'center'`, permettant de contrôler la disposition des graphiques par rapport au texte.
    

Ces options constituent les paramètres les plus fréquemment ajustés lors de la rédaction de documents avec `knitr` et R Markdown, offrant un contrôle précis sur l'exécution du code, l'affichage des résultats et la présentation des éléments graphiques.