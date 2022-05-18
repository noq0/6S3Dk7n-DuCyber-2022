# Mais quels sont ces fonctionnalités
# Sommaire 

- [Mais quels sont ces fonctionnalités](#mais-quels-sont-ces-fonctionnalités)
- [Sommaire](#sommaire)
- [Listes des sources ayant aidé pour la création de l'article :](#listes-des-sources-ayant-aidé-pour-la-création-de-larticle-)
  - [Etudes de cas, vidéos et articles](#etudes-de-cas-vidéos-et-articles)
  - [A travers la documentation elastic.co](#a-travers-la-documentation-elasticco)
- [Documentaiton et notes supplémentaires](#documentaiton-et-notes-supplémentaires)
  - [Présentation d'Elastic security](#présentation-delastic-security)

# Listes des sources ayant aidé pour la création de l'article :
## Etudes de cas, vidéos et articles
- Elastic Security - Unified Protection for Everyone - Aug 13, 2020 Elastic meetup : https://www.youtube.com/watch?v=eEmR1S2gVNY
- Qu'est-ce que X-Pack ? : https://www.elastic.co/fr/what-is/open-x-pack
- Endpoint Security Intergration vs. Windows and System Intergrations : https://discuss.elastic.co/t/endpoint-security-intergration-vs-windows-and-system-intergrations/295731
- Limitless XDR : ingérez, conservez et analysez gratuitement des données de sécurité : https://www.elastic.co/fr/blog/introducing-limitless-xdr 
- EDR ou XDR ? : https://www.elastic.co/fr/pdf/edr-xdr-checklist-2021.pdf
- Sécurité sans limites : https://www.elastic.co/fr/explore/security-without-limits
- presentation : https://blog.syone.com/elastic-security-unified-protection-for-everyone
- log forward elasticsearch : https://youtu.be/IKTpKCIbv3M?list=PL_mJOmq4zsHYod2PeZLLljkeXwKttSF_o&t=595

## A travers la documentation elastic.co
- Beats and Elastic Agent capabilities : https://www.elastic.co/guide/en/fleet/8.1/beats-agent-comparison.html
- Matrice de prise en charge des fonctionnalités elasticsearch : https://www.elastic.co/fr/support/matrix#matrix_compatibility
- Elastic Security overview : https://www.elastic.co/guide/en/security/master/es-overview.html

# Documentaiton et notes supplémentaires
## Présentation d'Elastic security

Elastic security est un nom commercial englobant plusieurs concepts autour de la sécurité informatique implémentés dans elasticsearch. </br>
L'objectif est de fournir des fonctionnalités d'un SIEM (Security Information and Events Management) à travers la suite Elastic grâce aux données intégrées, mais aussi de fournir des outils pour prévenir et agir lors d'attaque informatique. </br>
L'intégration des modules elastic security se fait de manière transversale sur la stack elasticsearch :
<p align="center">
  <img src="assets/elastic-security-01.png" width="60%"/>
</p>

L'entreprise a d'ailleurs fournit un flux de travail (workflow) permettant de comprendre que l'utilité du service peut s'étendre bien au delà d'une simple prévention / détection : il peut réellement servir à une équipe d'un centre d'opération de sécurité (SOC) :

[![Foo](https://www.elastic.co/guide/en/security/8.1/images/workflow.png)](https://www.elastic.co/guide/en/security/8.1/es-overview.html#_elastic_security_components_and_workflow)

Deux champs de tavail principal tourne autour d'elastic security :
- La récupération de données de l'hôte (télémétrie) vers elasticsearch.
- La gestion des règle de détection, des investigations cyber, et l'administration de Endpoint Security à travers l'agent Elastic.

Ces champs peuvent se lier aux concepts de cybersécurité. On peut :
- Investiguer seul ou à plusieurs (hunt team) sur des cas cyber en analysant les données présentes.
- Dététer et prévenir les intrusions en fonction d'une chaine d'évènements précis, via la détection d'une anomalie, ou d'un problème de sécurité.
- Créer soi même ou importer depuis la communauté des règles de détections/prévention d'intrusion
- Surveiller la santé des infrastructures.

Ci-dessous d'autres fonctionnalités possibles, exausthif, pas forcément étiqueté comme une solution de "elastic security":
- Pour la récupération de donnée dans ELK
  - On peut installer et utiliser sur l'hôte les modules Beats, à travers des intégrations. On peut utiliser Elastic endpoint et Elastic Endpoint Security
- Pour La gestion du flux de travail (workflow) :
  - Le moteur de détection des anomalies cyber permet :
    - Que des règles de détection d'anomalies peuvent être mises en place avec alertes email (un grand nombre sont prégénérés automatiquement dans la stack) En analysant régulièrement les données.
    - Le travail des faux positifs, des faux négatifs, et de la réduction du "bruit" généré par la quantité de donnée présentes.
    - La généreration des scores d'anormalités avec du machine learning.