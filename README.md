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

### Run2: Sac à mots + SVC

#### Description de la méthode:

- **Descripteurs utilisés:** Vecteurs Bag of Words obtenus à partir de la combinaison des titres et des ingrédients des recettes. Cette méthode compte la fréquence des mots dans chaque document.
- **Classifieur utilisé:** SVM (Support Vector Machine) avec un noyau linéaire. Le SVM a été choisi pour sa capacité à gérer la classification textuelle. L'utilisation d'un noyau linéaire vise à maintenir le modèle relativement simple.

**Choix de l'approche Sac à mots :**
Vous avez dit durant les seances, que nous avons le droit de regarder en ligne, comment les gens qui ont participés à cet événment ont pu resoudre la tache, à condition de le mentionner. Donc je suis parti voir et j'ai vu que le classifier SVM a toujours été utilisé donc j'ai voulu le tester pour voir si il me donnera une meilleur accuracy par rapport au logistic regression et j'ai aussi voulu changer l'approche qui va avec, donc j'ai utilisé les sac à mots au lieu de tf-idf, pour voir si ce changement donnera de meilleur resultats.

##### Résultats

| Run              | F1 Score (Macro) |
| ---------------- | ---------------: |
| TF-IDF + LR      |              83% |
| Sac à mots + SVC |              83% |
| METH 3           |                - |

### Run3: Word2Vec + RNN Simple

Description de la méthode:

- **Descripteurs utilisés:** Vecteurs générés par Word2Vec à partir de la combinaison des titres et des ingrédients des recettes.

- **Classifieur utilisé:** Un modèle de réseau de neurones récurrents (RNN) simple a été utilisé. Le modèle commence par une couche d'embedding, suivie d'une couche RNN simple pour traiter la séquence des mots, et se termine par des couches dense pour la classification.

**Choix de l'approche Word2Vec + RNN Simple :**
Les RNN, nous les avons vu en cours, et j'avais envie d'essayer
d'implementer un programme qui utilise les reseau de neuronne,
je me suis dit que ca sera forcement la methode la plus puissante, parmi tout ce qu'on a essayée mais en fait, elle etait la plus mauvaise,
car je pense qu'on a si peu de données et donc une methode aussi avancée, a besoin de beaucoup plus de données.

## Résultats Global

| Run              | F1 Score (Macro) |
| ---------------- | ---------------: |
| TF-IDF + LR      |              83% |
| Sac à mots + SVC |              83% |
| Word2Vec + RNN   |              73% |

### Analyse de résultats

L'analyse globale des résultats obtenus à travers les différentes approches révèle des informations intéressants sur la tâche de classification et sur les capacités des méthodes employées.

- **Performances des méthodes**: Les approches basées sur TF-IDF + Régression Logistique et Sac à mots + SVC ont montré des performances équivalentes, avec un score F1 macro de 83%. Cette égalité des performances suggère que pour notre jeu de données spécifique, la distinction entre les recettes en termes de catégories peut être efficacement capturée par des caractéristiques simples, comme la fréquence des mots et l'importance relative des termes dans le corpus.

- **Limitation de Word2Vec + RNN**: L'approche Word2Vec + RNN Simple a enregistré une performance inférieure avec un score F1 macro de 73%. Cette observation confirme l'hypothèse initiale discutée en cours avec le professeur que malgré la puissance des modèles basés sur les réseaux de neurones et les embeddings de mots, la quantité de données disponible joue un rôle important. Les RNN, en particulier, sont connus pour nécessiter de grandes quantités de données d'entraînement. Une contrainte qui a probablement limité la performance de cette méthode dans notre contexte.

### Pistes d'analyse

- **Manque de données**: Comme nous l'avons dit en haut, la quantité de données disponibles est un facteur limitant majeur pour l'approche Word2Vec + RNN. Ce qui nous montre l'importance de la disponibilité des données en IA, en particulier pour les approches basées sur les réseaux de neurones profonds qui nécessitent généralement un large ensemble de données d'entraînement pour capturer efficacement les patterns complexes.

- **Complexité des modèles**: La comparaison des performances entre les méthodes plus simples (TF-IDF + Régression Logistique, Sac à mots + SVC) et le modèle plus complexe (Word2Vec + RNN) indique que des modèles plus simples peuvent être préférables lorsque la taille du dataset est limitée. Cela peut être dû à leur capacité à éviter le surapprentissage et à mieux predire à partir de moins d'exemples.

### Conclusion et perspectives

Ce projet nous a permis de mieux comprendre l'impact des différentes méthodes de représentation textuelle et des modèles de classification sur la tâche de classification des recettes. Bien que les méthodes traditionnelles aient montré de bonnes performances, l'exploration de modèles plus avancés, tels que les RNN avec Word2Vec, reste un choix prometteur avec plus de données. Pour des travaux futurs, il serait intéressant de considérer des architectures de réseaux de neurones plus puissantes, telles que les LSTM ou les Transformers, et de trouver des moyens pour augmenter les données d'entraînement.
