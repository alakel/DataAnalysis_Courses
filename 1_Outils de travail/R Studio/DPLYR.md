## Fonctions de base
### 1. **`filter()`** : Filtrer des lignes selon des conditions
```R
# Filtrer les lignes où la colonne 'age' est supérieure à 30
df_filtered <- df %>% filter(age > 30)
```

### 2. **`select()`** : Sélectionner des colonnes spécifiques
```R
# Sélectionner les colonnes 'name' et 'age'
df_selected <- df %>% select(name, age)
```

### 3. **`mutate()`** : Créer ou modifier des colonnes
```R
# Ajouter une nouvelle colonne 'age_in_months' qui est 'age' multiplié par 12
df_mutated <- df %>% mutate(age_in_months = age * 12)
```

### 4. **`summarise()`** : Résumer des données avec des fonctions d'agrégation
```R
# Calculer la moyenne de la colonne 'age'
df_summary <- df %>% summarise(mean_age = mean(age, na.rm = TRUE))
```

### 5. **`group_by()`** : Grouper les données avant un calcul d'agrégation
```R
# Grouper par 'gender' et calculer la moyenne d'âge par groupe
df_grouped <- df %>% group_by(gender) %>% summarise(mean_age = mean(age, na.rm = TRUE))
```

### 6. **`arrange()`** : Trier les données
```R
# Trier par 'age' croissant
df_arranged <- df %>% arrange(age)

# Trier par 'age' décroissant
df_arranged_desc <- df %>% arrange(desc(age))
```

### 7. **`rename()`** : Renommer des colonnes
```R
# Renommer la colonne 'age' en 'years'
df_renamed <- df %>% rename(years = age)
```

### 8. **`count()`** : Compter le nombre d’occurrences dans un groupe
```R
# Compter le nombre de valeurs par 'gender'
df_counted <- df %>% count(gender)
```

### 9. **`distinct()`** : Retirer les doublons
```R
# Obtenir les lignes uniques
df_distinct <- df %>% distinct()
```

### 10. **`slice()`** : Extraire des lignes par position
```R
# Sélectionner les 5 premières lignes
df_sliced <- df %>% slice(1:5)
```

### 11. **`top_n()`** : Sélectionner les n plus grandes ou petites valeurs
```R
# Sélectionner les 3 plus grandes valeurs de 'age'
df_top <- df %>% top_n(3, age)
```

### 12. **`inner_join()`** : Jointure interne de deux tables
```R
# Joindre df1 et df2 sur la colonne 'id'
df_joined <- df1 %>% inner_join(df2, by = "id")
```

### 13. **`left_join()`** : Jointure externe gauche
```R
# Jointure externe gauche entre df1 et df2 sur 'id'
df_left_join <- df1 %>% left_join(df2, by = "id")
```

### 14. **`right_join()`** : Jointure externe droite
```R
# Jointure externe droite
df_right_join <- df1 %>% right_join(df2, by = "id")
```

### 15. **`full_join()`** : Jointure externe complète
```R
# Jointure externe complète entre df1 et df2
df_full_join <- df1 %>% full_join(df2, by = "id")
```

### 16. **`bind_rows()`** : Combiner des tables par lignes
```R
# Combiner df1 et df2 par les lignes
df_combined <- bind_rows(df1, df2)
```

### 17. **`bind_cols()`** : Combiner des tables par colonnes
```R
# Combiner df1 et df2 par les colonnes
df_combined_cols <- bind_cols(df1, df2)
```

### 18. **`across()`** : Appliquer des transformations à plusieurs colonnes
```R
# Appliquer la fonction 'mean' à plusieurs colonnes numériques
df_across <- df %>% summarise(across(where(is.numeric), mean, na.rm = TRUE))
```

### 19. **`if_else()`** : Appliquer des conditions logiques
```R
# Ajouter une colonne 'adult' basée sur la condition 'age >= 18'
df_ifelse <- df %>% mutate(adult = if_else(age >= 18, "Yes", "No"))
```

## II - Fonctions avancées pour data analyst

Chez les data analysts et data scientists spécialisés en **machine learning** (ML) et **deep learning** (DL), **`dplyr`** joue un rôle essentiel dans la **préparation des données**. Bien que `dplyr` ne soit pas directement lié aux algorithmes d'apprentissage automatique ou profond, il est fondamental pour **nettoyer**, **transformer** et **préparer les données** de manière efficace avant de les utiliser dans des modèles ML/DL. Voici un aperçu des usages plus avancés de `dplyr`, particulièrement pour les professionnels travaillant avec ces méthodes.

### 1. **Préparation des données pour l'entraînement de modèles**
La **qualité des données** est cruciale dans le succès d'un modèle de machine learning. `dplyr` est largement utilisé pour préparer les données en vue de leur utilisation avec des algorithmes d'apprentissage.

#### a. **Normalisation et standardisation des variables**
Dans les modèles ML/DL, il est souvent nécessaire de **normaliser** ou **standardiser** les variables. `dplyr` peut être utilisé pour appliquer ces transformations rapidement à plusieurs colonnes.

```R
# Normalisation : transformation des variables entre 0 et 1
df_normalized <- df %>%
  mutate(across(where(is.numeric), ~ (. - min(.)) / (max(.) - min(.))))
```

#### b. **Feature engineering** (Création de nouvelles variables)
La **création de nouvelles variables** à partir de celles existantes est un aspect essentiel du **feature engineering**. Cela peut inclure la combinaison de plusieurs colonnes, la création de variables indicatrices (dummy variables) ou encore l'extraction d'informations supplémentaires à partir de variables existantes.

```R
# Créer une nouvelle variable basée sur l'interaction de deux autres
df_features <- df %>%
  mutate(interaction_term = var1 * var2)
```

#### c. **Création de catégories** (binarisation, bucketing)
Les modèles de machine learning peuvent bénéficier de la **binarisation** ou de la **catégorisation** de certaines variables continues.

```R
# Créer des catégories basées sur l'âge
df_buckets <- df %>%
  mutate(age_group = case_when(
    age < 20 ~ 'Jeune',
    age >= 20 & age < 40 ~ 'Adulte',
    age >= 40 ~ 'Sénior'
  ))
```

### 2. **Gestion des données manquantes**
La gestion des données manquantes est un élément crucial de la préparation des données pour ML/DL. `dplyr` permet de manipuler facilement les **NA** dans un jeu de données.

#### a. **Remplir les valeurs manquantes**
Les valeurs manquantes peuvent être remplacées par des moyennes, médianes ou autres statistiques d'agrégation pour stabiliser l'entraînement d'un modèle.

```R
# Remplacer les NA par la médiane
df_filled <- df %>%
  mutate(across(where(is.numeric), ~ if_else(is.na(.), median(., na.rm = TRUE), .)))
```

#### b. **Filtrer les observations manquantes**
Dans certains cas, il peut être préférable de **supprimer** les lignes contenant des valeurs manquantes.

```R
# Supprimer les lignes avec des NA dans certaines colonnes
df_no_na <- df %>%
  drop_na(var1, var2)
```

### 3. **Transformation de données massives**
Pour les data analysts et data scientists qui travaillent avec des **datasets de grande taille**, `dplyr` fournit des outils efficaces pour **filtrer**, **muter** et **agréger** les données sans utiliser trop de mémoire. En utilisant des backends comme **`data.table`** ou des bases de données (via **`dbplyr`**), `dplyr` peut gérer des ensembles de données massifs.

#### a. **Manipulation de données dans des bases de données**
Avec `dplyr` et **`dbplyr`**, il est possible de manipuler des données directement dans des bases de données relationnelles, évitant ainsi de charger l'ensemble des données en mémoire.

```R
# Connexion à une base de données et manipulation directe
library(DBI)
con <- dbConnect(RSQLite::SQLite(), "my_database.sqlite")
df_db <- tbl(con, "my_table") %>%
  filter(age > 30) %>%
  summarise(mean_income = mean(income, na.rm = TRUE))
```

### 4. **Feature selection et importance des variables**
En machine learning, la **sélection des variables** (feature selection) est cruciale pour améliorer la performance des modèles. `dplyr` peut être utilisé en combinaison avec des techniques de **corrélation**, ou en s'appuyant sur des méthodes spécifiques à certains algorithmes comme **Random Forest**.

#### a. **Suppression des variables à faible variance**
Supprimer les variables avec très peu de variance (par exemple, les colonnes qui sont majoritairement constantes) peut réduire le bruit dans les données.

```R
# Supprimer les colonnes dont la variance est inférieure à un certain seuil
df_filtered_variance <- df %>%
  select(where(~ var(.) > 0.01))
```

### 5. **Gestion des jeux d'entraînement et de test**
Le processus d'entraînement d'un modèle ML nécessite souvent de diviser les données en **jeux d'entraînement** et **jeux de test**. Bien que cette tâche soit souvent réalisée avec des packages dédiés comme **`caret`**, `dplyr` peut être utilisé pour créer ces splits.

```R
# Diviser les données en jeux d'entraînement (70%) et de test (30%)
set.seed(123)  # Fixer une graine pour la reproductibilité
train_indices <- sample(nrow(df), 0.7 * nrow(df))
df_train <- df %>% slice(train_indices)
df_test <- df %>% slice(-train_indices)
```

### 6. **Agrégation de données pour la validation croisée**
La validation croisée (cross-validation) est couramment utilisée en machine learning pour évaluer les performances des modèles. `dplyr` peut être utilisé pour **agréger les résultats** de multiples modèles entraînés sur différents jeux de données.

```R
# Simuler plusieurs modèles et agréger les résultats des prédictions
results <- df %>%
  group_by(fold) %>%
  summarise(mean_accuracy = mean(accuracy))
```

### 7. **Intégration avec des pipelines machine learning**
`dplyr` s'intègre bien avec des frameworks de machine learning comme **`caret`** ou **`parsnip`** pour la création de **pipelines de modélisation**. Ces packages prennent souvent les objets manipulés par `dplyr` et appliquent des modèles prédictifs directement.

```R
# Exemple d'intégration avec le package parsnip
library(parsnip)

model <- linear_reg() %>%
  set_engine("lm") %>%
  fit(Sepal.Length ~ Sepal.Width, data = df %>% filter(Species == "setosa"))
```

