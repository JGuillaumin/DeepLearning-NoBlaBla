# Instructions d'installation 


Il s'agit des instructions pour les personnes souhaitant installer l'environnement de travail sur leur machine. 

**Note**: Ceci n'est pas obligatoire ! Vous pouvez très bien venir à l'atelier avec votre ordinateur sans rien installer.
Il faudra juste se connecter à des machines à distance (chez Amazon) depuis un navigateur.
(votre ordinateur doit pouvoir se connecter au Wifi et avoir un navigateur récent)


Pour les plus courageux, voici quand même les instructions d'installation !


**Rq** : Pour l'instant ces instructions ne concerne que Linux (et Mac pour certaines méthodes)!
Je suis encore en train de faire des tests pour Windows. 


Plusieurs options s'offrent à vous ! 
 - Déjà, CPU ou GPU ? 
 - Dans un container Docker ou directement sur la machine ? 

Les librairies de Deep Learning fonctionnent très bien avec les cartes graphiques Nvidia ! 
On a au minimum un facteur x10 en rapidité lors de l'apprentissage sur un GPU (un peu moins pour l'inférence). 

Malheureusement si votre portable est équipé d'une carte graphique, il est difficile de travailler avec sous Linux ! 
Il a des problèmes de compatibilité matériel, des problèmes pour les drivers ... 
Ce n'est pas simple ! 

Donc si vous êtes équipé d'une carte graphique Nvidia, mais que vous n'avez pas des drivers récents (>=352.xx) je vous conseille de partir sur les instructions d'installation pour CPU ! 
(je vais quand même rajouter en fin de page les astuces pour installer des drivers Nvidia récents)


## Docker sur CPU (Linux et Mac) 

#### Installer Docker 

Pour ça je vous renvoie vers la page d'installation de Docker: https://docs.docker.com/engine/installation/
Pas besoin d'être un expert en Docker, le dockerfile proposé est bien construit, tout se lancera automatiquement ! 

#### Construire l'image

Il d'abord cloner ce repo GitHub, puis se déplacer dans `install/`. 
Il suffit de lancer la commande : 

```bash
docker build -f Dockerfile.cpu -t myname/no-blabla:cpu .
```

**Etapes**: 
Cette commande lance la construction de l'image : 
 - Elle part de l'image officielle Ubuntu16.04
 - On y installe les dépendances nécessaires pour Python3, Keras et TensorFlow.
 - Puis télécharge et installe `Miniconda`, un gestionnaire d'environnements virtuels Python !
 - Les dépendances Python (sklearn, pandas, Keras, ...) sont installer dans un 'virtual env' nommé `no-blabloa`.
 - On choisit `/src/` comme répertoire de travail 
 - Enfin on ajoute un script bash qui lancera automatiquement Jupyter dans le bon 'virtual env' python !


La construction peut prendre du temps (~1h) donc patience (et à ne faire 30 minutes avant le début de l'atelier).
L'image construite fait 2.7GB !!  

#### Lancer le container 

Placez-vous à la racine du projet (devant `install`, `part1`, `part2`, ...) et lancez : 

```bash
docker run -it -p 8888:8888 -p 7000:7000 -v "$PWD"/:/src myname/no-blabla:cpu 
```

Vous pouvez directement aller dans votre navigateur Internet : `localhost:8888/`
(le port 7000 est utile pour le serveur web de Quiver, qui permet de faire de la visualisation de CNNs!)


Et voilà ! 



## Docker sur GPU (pour confirmé(e) sur Linux)

L'image pour GPU utilise CUDA 8.0 ! 
Il faut donc avoir des drivers récents : >=352.xx 


**RQ** : 
- Je n'ai pas réussi à créer une image pour GPU stable sous Python 3.5 (kernel python instable ou GPU non utilisé)
- Cette image utilise donc Python 2.7 ! 
- Mais le code dans les notebooks est compatible 2.7 et 3.5 . (dès que je trouve une solution pour Python 3.5, je la partage ici) 


#### Installer Docker et nvidia-docker

Il faut tout d'abord installer Docker, puis `nvidia-docker` : https://github.com/NVIDIA/nvidia-docker
Il faut suivre les instructions sur la page principale (évitez de re-compiler à partir des sources comme proposé sur la page 'installation').
Il s'agit d'un outil supplémentaire qui permet à Docker d'avoir accès au GPU ! 

#### Construire l'image 

```bash
docker build -f Dockerfile.gpu -t myname/no-blabla:gpu .
```

#### Lancer le container docke 

Placez-vous à la racine du projet, puis : 

```bash
nvidia-docker run -it -p 8888:8888 -p 7000:7000 -v "$PWD"/:/src myname/no-blabla:gpu 
```

Puis allez sur `localhost:8888` dans votre navigateur Internet ! 



## Anaconda sur CPU (Linux, Mac, pas encore testé sur Windows)

Installez Anaconda pour Python 3.5 : https://www.continuum.io/downloads
(toutes les instructions sont sur la page)

Puis dans le répertoire `install` :

```bash
conda env create -f environment.yml
 ```

Activez l'env créé et lancez Jupyter: 

```bash
source activate no-blabla
jupyter notebook &
```


**Rq** : ces commandes concernent Linux (et Mac), pour Windows il faut les adapter pour créer le même environnement virtuel à partir du même fichier `environment.yml`.



