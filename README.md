# DEFT2013 Tâche 2 : Classification des Recettes de Cuisine

AL ADDAM Besher - BOUSTILA Firas

## Description de la tâche

La tâche consiste à développer un système capable de classifier automatiquement des recettes de cuisine en trois catégories : Dessert, Entrée, et Plat principal, en se basant sur les titres et ingrédients des recettes.

### Exemples de documents

- **ID:** 217204

  - **Titre:** Crêpes au canard laqué
  - **Ingrédients:** farine - maïzena - œufs - lait - hoisin - 1 cuillère à soupe de vin
  - **Catégorie:** Dessert

- **ID:** 55831
  - **Titre:** Tourte lorraine
  - **Ingrédients:** farine - beurre - escalopes de veau - jaune d'œufs - noix de beurre - sel - poivre
  - **Catégorie:** Entrée

## Statistiques corpus

- **Nombre de documents de train/test:** 12473/1388
- **Répartition des étiquettes dans chacun des sous-ensembles:**
  - **Train:** Dessert (40%), Entrée (30%), Plat principal (30%)
  - **Test:** Dessert (35%), Entrée (30%), Plat principal (35%)

## Méthodes proposées

### Run1: TF-IDF + Régression Logistique

#### Description de la méthode:

- **Descripteurs utilisés:** Vecteurs TF-IDF obtenus à partir de la combinaison des titres et des ingrédients des recettes.
- **Classifieur utilisé:** Régression Logistique, choisie pour sa simplicité et son efficacité dans les tâches de classification. Un maximum de 3000 itérations a été spécifié pour assurer la convergence du modèle.

Choix de la **Cross-Validation:** pour l'apprentissage:

Durant le cours de machine learning, j'ai appris la méthode de cross-validation. Cette méthode m'a réellement marqué, car j'avais l'impression qu'il s'agissait d'une technique extrêmement puissante. Lorsque vous avez annoncé le projet à réaliser, c'est vers la cross-validation que mes pensées se sont tournées. J'avais l'impression que cette approche me permettrait non seulement d'avoir un très bon modèle mais également de me démarquer par rapport aux autres groupes. Avec cette technique de cross-validation, je me suis dit que je pourrais atteindre une excellente précision, et donc bien réussir ce projet.

##### Résultats

| Run         | F1 Score (Macro) |
| ----------- | ---------------: |
| TF-IDF + RL |              83% |
| METH 2      |                - |
| METH 3      |                - |
| METH 4      |                - |

### Run2: Sac à mots + SVC

#### Description de la méthode:

- **Descripteurs utilisés:** Vecteurs Bag of Words obtenus à partir de la combinaison des titres et des ingrédients des recettes. Cette méthode compte la fréquence des mots dans chaque document.
- **Classifieur utilisé:** SVM (Support Vector Machine) avec un noyau linéaire. Le SVM a été choisi pour sa capacité à gérer la classification textuelle. L'utilisation d'un noyau linéaire vise à maintenir le modèle relativement simple.

**Choix de l'approche Sac à mots :**
Vous avez dit durant les seances, que nous avons le droit de regarder en ligne, comment les gens qui ont participés à cet événment ont pu resoudre la tache, à condition de le mentionner. Donc je suis parti voir et j'ai vu que le classifier SVM a toujours été utilisé donc j'ai voulu le tester pour voir si il me donnera une meilleur accuracy par rapport au logistic regression et j'ai aussi voulu changer l'approche qui va avec, donc j'ai utilisé les sac à mots au lieu de tf-idf, pour voir si ce changement donnera de meilleur resultats.

##### Résultats

| Run              | F1 Score (Macro) |
| ---------------- | ---------------: |
| TF-IDF + RL      |              83% |
| Sac à mots + SVC |              83% |
| METH 3           |                - |

### Run3: NOMMETHODE

## Résultats Global

| Run              | F1 Score (Macro) |
| ---------------- | ---------------: |
| TF-IDF + RL      |              83% |
| Sac à mots + SVC |              83% |
| METH 3           |                - |

### Analyse de résultats

#### Pistes d'analyse:

- **Performance par catégorie:** La classification des Desserts a montré des performances élevées, alors que la distinction entre Entrées et Plats principaux a été plus difficile pour le modèle, ce qui veut dire qu'il reste des pas d'amélioration à faire dans ces deux catégories.
- **Matrice de confusion:** La matrice de confusion a révélé des confusions notables entre les Entrées et les Plats principaux, suggérant que le modèle peut bénéficier d'une meilleure distinction des caractéristiques ou d'une augmentation des données d'entraînement pour ces catégories.

#### Conclusions et perspectives:

Le modèle de base a démontré une capacité solide à classifier les recettes avec une précision globalement élevée. Pour améliorer davantage la performance, des méthodes supplémentaires pourraient inclure l'utilisation d'embeddings de mots plus sophistiqués, l'expérimentation avec des modèles de deep learning, ou l'introduction de caractéristiques supplémentaires telles que la longueur de la recette ou le nombre d'ingrédients. Des études futures pourraient également explorer des stratégies de regroupement des ingrédients en catégories plus larges pour améliorer la distinction entre les types de recettes.
