# Instructions d'installation 

Il s'agit des instructions pour les personnes souhaitant installer sur leur ordinateur toutes les librairies. 

Pour les autres, aucun problème, nous fournissons des instances Amazon AWS, équipée de GPU et avec toutes les librairies pour la soirée.
C'est d'ailleurs la solution Amazon que je préconise pour la soirée !
(il faut juste ramener son ordinateur, le connecter en Wifi et avoir un navigateur récent, type Chrome ou Firefox)


Pour les plus courageux, voici quand même les instructions d'installation !

Pour les personnes travaillant sous Linux, Mac (et Windows je pense, je n'ai pas testé), je vous propose d'utiliser une image Docker déjà préparée : 
- `udacity/carnd-term1-starter-kit`

Pas besoin d'être un expert en Docker ! 
Pour l'installation de Docker je vous envoie vers le site officiel : https://docs.docker.com/engine/installation/


### Etape 1 : Télécharger l'image 

Il s'agit d'une image Docker préparée par le MOOC "Self-driving cars" proposé par Udacity. 
Elle contient toutes les librairies pour la soirée. 

```bash
docker pull udacity/carnd-term1-starter-kit
```

### Etape 2 : Récupérer les notebooks et les données 

Vous pouvez faire un clone du repo Github pourrécupérer uniquement les notebooks. 
Mais vous pouvez attendre la soirée où je vais faire circuler des clefs USB avec les notebooks et les données ! 


### Etape 3 : Lancer l'image 

Placez-vous à la racine du projet, là où se trouvent les répertoires (part1, part2, ...).
Puis : 

```bash
docker run --it -p 8888:8888 -v "$PWD"/:/src udacity/carnd-term1-starter-kit
```

Le container lance directement Jupyter, vous n'avez plus qu'à vous rendre sur `localhost:8888` dans votre navigateur préféré. 
