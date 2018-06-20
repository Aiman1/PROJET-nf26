# Objectifs (idéaux)

Construire un DW pour stocker les données électorales, et les méthodes d'analyse associées.

# Données

* Données électorales des élections legislatives (se limiter à la période 90-présent, en éliminant les partielles), disponnibles [ici](https://www.data.gouv.fr/fr/posts/les-donnees-des-elections/), conseil utiliser les données dun ministère de l'intérieur.
* Toutes données de l'[INSÉÉ](https://statistiques-locales.insee.fr/#c=indicator) jugées pertinentes.

# Analyse

Il s'agira de pouvoir répondre aux questions suivantes:

* Taux lors d'un suffrage
    * de vote (ou abstention) à tous les niveaux de granularité géographiques appropriés et disponnibles (bureaux, commune, dpt…)
    * scores pour les différents mouvements politiques
* Évolution entre les suffrages des taux précités.
* Analyser le vote/abstension et le scores des mvt politiques en fonction de d'indicateurs socio-économiques, p.ex.
    * Revenu médian
    * Taux de chomage
    * Niveau d'étude…

Concernant les changements de nom des formations politiques : il faut le prendre en compte (comment ? À vous de voir).

# Attendu

Principal :

* Modélisation du problème (cf première partie). Cette modélisation n'est pas l'essence de ce projet, ce point devra être traité rapidement.
* La matérialisation des données (ou les multiples matérialisations d'icelles), sous forme de concept. C'est à dire, distribution des données, clef de partitionnement/tri, organisation, etc. Justification, pour chaque type d'analyse imaginée.
* Les méthodes d'analyse (et de comptage) à l'aide d'algo distribués (comme du map et reduce), ou au minimum travaillant en streaming (c'est à dire, sans stocker toutes les données), sous forme de concept.

Secondaire (mais vraiment secondaire, je sais bien que le projet est court, donc je n'ai peu d'espoir) :

* L'implémentation de la matérialisation
* L'alimentation
* L'implémentation des méthodes d'analyse

# Rendu

Oral:

* 5 min par binôme, 2 slides.
* Je veux principalement une explication de la modélisation et de la matérialisation et surtout des choix effectués pour cette matérialisation.
* La semaine prochaine, jeudi ou vendredi, planning à venir.

Écrit:
* rapport synthétique de 6 pages (surface totale maximum 3750cm², pour ceux qui pensaient rendre en A3),
* annexes autorisées, les annexes doivent être courtes, pertinente, mais non essentielles, et chaque annexe doit être référencée par le rapport, du code se fournit en annexe sans se mettre dans un pdf.
* Vendredi prochain, samedi autorisé.

