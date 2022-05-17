# Les alertes et les tableaux de bords

# Sommaire

- [Les alertes et les tableaux de bords](#les-alertes-et-les-tableaux-de-bords)
- [Sommaire](#sommaire)
- [Sources](#sources)
- [Documentaiton et notes supplémentaires](#documentaiton-et-notes-supplémentaires)
  - [Récupérer des virus connus sur internet et effectuer des actions malicieuses](#récupérer-des-virus-connus-sur-internet-et-effectuer-des-actions-malicieuses)

# Sources

- EQL Search : https://www.elastic.co/guide/en/elasticsearch/reference/8.2/eql.html
- Kibana Query Language : https://www.elastic.co/guide/en/kibana/7.6/kuery-query.html
- toute les règles de détection sur elastic Security : https://github.com/elastic/detection-rules
- liste des mises à jour de ces règles : https://www.elastic.co/guide/en/security/current/prebuilt-rules-downloadable-updates.html

# Documentaiton et notes supplémentaires

## Récupérer des virus connus sur internet et effectuer des actions malicieuses

Pour générer de la télémétrie et des données de sécurité à travers elasticsearch, nous pouvons récupérer un lots de virus sur internet. Il en va de soi qu'il est possible d'en récupérer par des moyens divers : des Honeypots, des emails de phishings précédents, scanner internet... un exemple de récupération de viruses se trouves ici : https://www.pcmag.com/about/how-we-collect-malware-for-hands-on-antivirus-testing

Nous effectuerons nos recherches directement sur les sites organisant la collecte d'artefacts vérolés. de çà à nous permettre de gagner du temps plustôt que de générer nos propres viruses.  par exemple une recherche google dork amélioré comme celle-ci `site:www.hybrid-analysis.com "hxxp"` peux nous donner toute les pages référencées par google, dont le site internet d'analyse antiviral Hybrid-Analysis a enregistré un lien HTTP. De par cette requête nous pourrions télécharger les artefacts vérolés à partir des liens proposés. Attention tout de même à ne pas effectuer vos recherches directement sur votre navigateur internet, mais plustôt de passer par une VM préparé pour cet effet. Une liste d'addresse IP, et de viruses peut être fait pur les envoyer au banc de test (VM de test Hôte de notre projet).

Quelles autres actions malicieuses peuvent être effectuées ? On peut modifier des clefs de registre critique, baisser la sécurité des protocoles... On peut aussi lister les règles présentes dans elasticsearch et tenter de les actionner en intervenant sur l'hôte... Tout est en réalité très varié, et tout lister reviendrait à effectuer le travail d'un cyber analyste.
