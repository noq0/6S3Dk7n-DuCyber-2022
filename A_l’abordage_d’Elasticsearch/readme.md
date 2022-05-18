# A l’abordage d’Elasticsearch
# Sommaire
- [A l’abordage d’Elasticsearch](#a-labordage-delasticsearch)
- [Sommaire](#sommaire)
- [Listes des sources ayant aidé pour la création de l'article :](#listes-des-sources-ayant-aidé-pour-la-création-de-larticle-)
  - [Etudes de cas, vidéos et articles](#etudes-de-cas-vidéos-et-articles)
  - [documentation elasticsearch](#documentation-elasticsearch)
- [Documentation additionelle](#documentation-additionelle)
  - [Présentation d'Elastic Stack](#présentation-delastic-stack)
  - [GLOSSAIRE et concepts elasticsearch](#glossaire-et-concepts-elasticsearch)

# Listes des sources ayant aidé pour la création de l'article :
## Etudes de cas, vidéos et articles
- Everything you Always Wanted to Know about Filebeat * But Were Afraid to Ask : https://www.youtube.com/watch?v=ykuw1piMGa4
- Beginner's Crash Course to Elastic Stack : https://www.youtube.com/playlist?list=PL_mJOmq4zsHZYAyK606y7wjQtC0aoE6Es
- Table of Contents: Beginner's Crash Course to Elastic Stack Series : https://github.com/LisaHJung/Beginners-Crash-Course-to-Elastic-Stack-Series-Table-of-Contents
- Elastic's Guide to Data Visualization in Kibana - May 15, 2020 Elastic Meetup : https://www.youtube.com/watch?v=e1299MWyr98
- Does Elasticsearch lie? How does Elasticsearch work? - https://medium.com/swlh/does-elasticsearch-lie-how-does-elasticsearch-work-f2d4e2bf92c9

## documentation elasticsearch
- Upgrade to the Elastic APM integration : https://www.elastic.co/guide/en/apm/guide/current/upgrade-to-apm-integration.html 
- elastic ecosystem : https://youtu.be/8JAHxtnZYOI?list=PL_mJOmq4zsHYod2PeZLLljkeXwKttSF_o&t=2085


# Documentation additionelle
## Présentation d'Elastic Stack

Anciennement appelé "Stack ELK" le produit phare proposé par l'entrprise Elastic NV, est la "stack elastic", en français, la "suite elastic". </br>
Composé de quatres produits principaux : Elasticsearch, Kibana, Beats et Logstash. </br>
Son principal but est "*de collecter n'importe quel format de données depuis n'importe quelle source, puis d'interroger, d'analyser et de visualiser vos données en temps réel.*"[^1]. Autrement dit, Un outil très intéressant dans le monde du big data. </br>
On retiendras rapidement la fonctionnalité de ces outils et leur interconnectivité évidente : </br>
- Elasticsearch est une base de donnée et un moteur de recherche construit initialement à partir de l'outil Apache Lucene. Il est interrogeable via une API REST. 
- Kibana est un outil de visualitation de données. Ces fonctionnalités en font un vraie site internet. Il permet d'interroger la base elasticsearch, d'en générer des graphiques et de les représenter dans des vues. Il est le principal outil d'interaction graphique avec la suite Elastic, et permets  aussi de configurer tout les outils nécéssaires à l'intégration de donnée et à l'administration de la stack.
- Logstash est un service d'ingestion et de tri de donnée. Il ingère n'importe quelle données de multiples sources en simultané, il la trie, la transforme, et l'envoi directement au serveur elasticsearch ou à d'autres sources dans un format lisible pour la destination. Il est installé côté serveur.
- De leur nom commercial, "Beats" sont des agent de transfert de donnée. Concu pour être installé au plus près de la donnée, sur un serveur ou sur une machine physique (côté "client"), leur particularité est d'ingérer les données à la source et de les transférer soit à elasticsearch soit à logstash. Plusieurs versions de Beats sont actuellement utilisées, toute avec des caractéristiques différentes[^2].

Cette Suite permets ainsi l'ingéstion de donnée de tout bord, sans structuration, et l'analyse de ces données "en masse". Certains concepts "d'index", de "flux de données" de "jobs" , de "librairie de visualisation", ainsi que les termes "elastic common shema", "pipeline logstash" sont à comprendre et à prendre en compte quand on utilise la stack entière.

Durant la création de ce projet, j'ai remarqué quelques outils qui n'étaient pas présentés mais étaient nécéssaires à la réalisation du projet.
Ces outils sont "transversaux" et sont peut mis en avant dans la documentation, ce qui complexifie la mise en place du projet. Voici une rapide présentation pour comprendre leur utilisation dans la suite du document :
- Fleet est un service qui propose une gestion centralisé des agents elasticsearch. La notion d'agent a été indroduite dans elasticsearch afin de pouvoir automatiser l'installation, la configuration et les mises à jour des outils qui permettent la remontée d'information (elastic agent gère l'installation et la configuration des agents Beats, mais aussi des fonctionnalités sécurité de la Stack sur les points de récolte d'information). Une interface sur Kibana, permet d'utiliser la console d'administration et de générer des configurations pour les agents elastic.
- Xpack est un ensemble programmes qui ajoutent des fonctionnalités multiples à la stack.  Nécéssaires pour une mise en production du produit, sa sécurité, son ergonomie... Xpack contient aussi des fonctionnalités toutes utiles et intéressantes, dont certaines sont réservés à des usages payants. La stack et un ensemble de fonctionnalités sont ouverte pour une utilisation gratuite et basique, mais très limité. Voici une liste non exausthive des thèmes de fonctionnalités ajoutées par xpack :
  1. Xpack Security
  2. Xpack Moniroting
  3. Xpack alerting
  4. Xpack reporting
  5. Xpack Machine learning
  6. Xpack Graph
  7. Xpack SQL

Voici le lien pour connaitre si la fonctionnalité utilisée est payante : https://www.elastic.co/fr/subscriptions. Il faut néamoins faire attention l'orsqu'on configure la Stack Elastic sur un serveur, car la simple activation d'une fonctionnalité considéré payante peut bloquer l'accès à toute la solution, et la rendre inutilisable tant que celle-ci n'a pas été désactivé.

[^1]: https://www.elastic.co/fr/elastic-stack/.
[^2]: https://github.com/elastic/beats

## GLOSSAIRE et concepts elasticsearch 

- Mappings : define how to store and index documents in elasticsearch
- Index settings : behavior of indices
- Lyfecycle policy : politique du cycle de vie
- Data streams : A data stream lets you store append-only time series data across multiple indices while giving you a single named resource for requests. un object appelé flux de donnée qui regroupe tout les indices associés à cet objet : utile lorsque es fichiers de logs sont trops longs, et qu'ils est nécéssaire de les diviser en plusieurs petits indexes. 
- Indices : equal to the concept of database
- Types : equal to tables in a classic database
- Documents : equal to rows in a classic database
- Properties : equal to a comumn in a classical database.
- data view : vue de donnée (permet de définir les données qui seront visible et qui permetterons de faire des recherches dans kibana.
An Elasticsearch cluster can contain multiple Indices (databases), which in turn contain multiple Types (tables). These types hold multiple Documents (rows), and each document has Properties(columns).


data view contains Data streams(multiples indices) and standalone indices.


