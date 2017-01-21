
Lors de l'atelier nous allons travailler avec 3 datasets disponibles sur Kaggle.com

Pour les télécharger il faut être connecté et accepter les conditions des compétitions concernées !


## Digit-Recognizer : https://www.kaggle.com/c/digit-recognizer

- Télécharger les deux fichiers CSV (`test.csv` et `train.csv`)
- Les placer dans `data/digit-recognizer/`
- Ouvrir le notebook `prep_data.ipynb` et exécuter les cellules pour préparer les données ! 


## CIFAR-10

Pour ce dataset, je suis parti des données disponibles sur Keras ! 
Il faut juste exécuter les cellules du notebook `data/CIFAR-10/prep_data.ipynb`. 

Le code va télécharger le dataset CIFAR-10 via Keras. 
Puis enregistrer les données dans tableaux Numpy (à faire avant l'atelier, le téléchargement peut être long!).


## Cats & Dogs : https://www.kaggle.com/c/dogs-vs-cats

Pour ce dataset, on va réduire les données (100x100) et créer l'arborescence suivante : 

- train_resize/cats/*.jpg
- train_resize/dogs/*.jpg
- test_resize/*.jpg

(la façon de ranger les données de cette manière va nous permettre d'utiliser un outils de Keras qui permet de gérer des gros datasets et de faire de l'augmentation de données à la volée ! 

- Télécharger `test.zip` et `train.zip` depuis Kaggle.com
- Les placer dans `data/cats-dogs/`
- Unzip
- Ouvrir le notebook de préparation des données : `prep_data.ipynb`
- Exécuter les cellules 

