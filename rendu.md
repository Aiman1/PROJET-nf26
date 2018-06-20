# Projet NF26
Guillaume JORANDON, Aiman Zaki

## Modélisation du problème

Pour modéliser le data-warehouse, nous avons décidé de considérer d'abord trois dimensions d'une modélisation en étoile :
* Spatiale : découpage géographique à toutes les granularités disponibles (bureau de vote, commune, etc.) ;
* Temporelle : découpage temporelle en tours et années ;
* Politique : découpage politique à toutes les granularités disponibles (candidat, parti).

La table de faits stocke alors le nombre de votes pour un candidat donné. Deux problèmes se posent alors dans la modélisation. D'une part, comment compter les votes blancs, nuls, et l'abstention ? D'autre part, comment prendre en compte les critères socio-économiques ?

Pour le premier problème, on le résout assez simplement en considérant Mr. (votes blancs), Mr. (votes nuls) et Mme. (abstention) comme des candidats. En revanche, il est difficile de répondre au deuxième problème avec une modélisation en étoile classique. En effet, on a vu sur le site de l'Insee que les critères socio-économiques sont répertoriés par emplacement géographique et par année. On décide donc de s'écarter un peu de la modélisation en étoile en ajoutant une entité "CSE", à cheval sur les dimensions temporelle et spatiale. On obtient ainsi la modélisation ci-dessous.

![](mcd.jpg)

TODO : ajouter le tour au découpage temporel et supprimer canton, supprimer orientation politique aussi

L'alimentation des différentes dimensions se fait en utilisant les données de l'Insee pour les critères socio-économiques (on prend directement les données par commune, qui est la granularité disponible la plus fine), et les données du Ministère de l'Intérieur pour les votes et les candidats.

## Matérialisations des données

On se pose plusieurs questions sur ces données, questions qui vont nécessiter plusieurs matérialisations différentes.

### Table 1 : Partitionnement pour les taux de vote par géographie

On choisit comme clef `(region, departement, annee, tour), circonscription, commune, candidat` pour avoir un partitionnement à tous les niveaux de granularité géographique, par année et par tour. On stocke dans les colonnes le nombre de votes. Cette matérialisation nous permettra de traiter taux de vote et d'abstention pour tous les niveaux de granularité géographique. Cette matérialisation nous permet aussi d'observer 

FIXME ou consolider en supprimer candidat de la clef de tri, et en ayant en colonnes nombre votes exprimés, nombre votes blancs, nombre votes nuls, nombre abstention

### Table 2 : Partitionnement pour les scores des mouvements politiques

On choisit comme clef `(departement, annee, tour), parti` pour avoir un partitionnement par département, année et tour. On stocke dans les colonnes le nombre de votes, ce qui nous permet de répondre aux questions sur les scores pour les différents mouvements politiques. La question posée ne concerne pas de variation du score selon la géographie, mais on a quand-même décider de partitionner les données par département afin de pouvoir avoir un aperçu des variations de score en fonction du département.

### Table 3 : Partitionnement pour les critères socio-économiques en fonction du parti

On choisit comme clef `(annee, tour), commune, parti` pour avoir un partitionnement par année et tour. On stocke dans les colonnes le nombre de votes et les critères socio-économiques associés à la commune, ce qui nous permet de répondre aux questions concernant les profils des électeurs en termes de critères socio-économiques, en fonction du mouvement politique.

### Table 4 : Partitionnement pour les critères socio-économiques en fonction du vote/abstention

On choisit comme clef `(region, departement, circonscription, annee, tour), commune, candidat` pour avoir un partitionnement à tous les niveaux de granularité géographique, par année et par tour. On stocke dans les colonnes le nombre de votes le nombre de votes et les critères socio-économiques, ce qui nous permet de traiter les taux de vote/abstention en fonction de critères socio-économiques.

## Méthodes d'analyse
