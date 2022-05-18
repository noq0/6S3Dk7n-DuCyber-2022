# L’infrastructure pour tester
# Sommaire
- [L’infrastructure pour tester](#linfrastructure-pour-tester)
- [Sommaire](#sommaire)
- [Listes des sources ayant aidé pour la création de l'article :](#listes-des-sources-ayant-aidé-pour-la-création-de-larticle-)
  - [Etudes de cas, vidéos et articles](#etudes-de-cas-vidéos-et-articles)
  - [documentation elasticsearch](#documentation-elasticsearch)
  - [outils](#outils)
- [Documentaiton et notes supplémentaires](#documentaiton-et-notes-supplémentaires)
  - [Configurer la suite elastic Checklist](#configurer-la-suite-elastic-checklist)
  - [Préparation de l'hôte Windows - Checklist](#préparation-de-lhôte-windows---checklist)
    - [1. Basique](#1-basique)
    - [2. Ajouts et modifications aux choix en fonction des besoins](#2-ajouts-et-modifications-aux-choix-en-fonction-des-besoins)
  - [Installer elasticsearch avec un serveur debian](#installer-elasticsearch-avec-un-serveur-debian)
    - [Installation de la suite ELK open source et ajout de Elastic security dans kibana](#installation-de-la-suite-elk-open-source-et-ajout-de-elastic-security-dans-kibana)
      - [Caractéristique de la VM pour les tests :](#caractéristique-de-la-vm-pour-les-tests-)
      - [Procédure d'installation sur debian](#procédure-dinstallation-sur-debian)
      - [Première connexion web au service kibana](#première-connexion-web-au-service-kibana)

# Listes des sources ayant aidé pour la création de l'article :
## Etudes de cas, vidéos et articles
- https://isc.sans.edu/forums/diary/Malware+Analysis+with+elasticagent+and+Microsoft+Sandbox/27248/
- https://www.elastic.co/fr/blog/how-to-build-a-malware-analysis-sandbox-with-elastic-security
- 

## documentation elasticsearch
- Installing the elastic stack : https://www.elastic.co/guide/en/elastic-stack/current/installing-elastic-stack.html

## outils
- Flare VM : https://github.com/mandiant/flare-vm 

# Documentaiton et notes supplémentaires
## Configurer la suite elastic Checklist

- Créez un namespace personnalisé pour attribuer toute les données récupérées sur ce namesapce
- Déployer l'agent Elasticsearch
- Ajouter les intégrations avec la liste des intégrations non exausthive (au minimum l'intégration elastic security).
- Configurer la politique de paramètres pour endpoint security.
- configurer votre moteur de détection Elastic (étiquetées comme règles).
- Activer toute les règles de détection

## Préparation de l'hôte Windows - Checklist

### 1. Basique
- S'assurer d'utiliser une VM configuré avec les politiques de l'entreprise
- S'assurer de logger correctement les informations suivantes, par exemple en préconfigurant les postes à travers les stratégies de groupe :
  - Ce qui est exécuté à travers powershell : </br> 
    https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.1
  - Configurer correctement la stack elastic dans le cas de l'utilisation d'elastic endpoint security
  - On peut activer l'isolation de l'hôte dans elastic security : va déconnecter d'internet l'application, mais va laisser la connexion vers kibana.

### 2. Ajouts et modifications aux choix en fonction des besoins
- On pourras ajouter quelques outils pour analyser ce qu'il s'est passé sur la machine et débugger.
- Désactiver les protections intégrées du système d'exploitation.
- Ajouter un domaine à la machine
- Scripts , configurations et programmes listés dans la Flaire VM : https://github.com/mandiant/flare-vm
- MS SysMon - MS TCPView : https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon - https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview
- Wireshark pour capturer le traffic sur l'hôte
- Navigateurs internet et outils : Chrome & Firefox - office - outils calssique de poste de travail
- PeStudio : https://www.winitor.com/features/
- Python
- Internet Services Simulation Suite: INetSim : https://www.inetsim.org/documentation.html
- Didier Stevens suite of tools : https://blog.didierstevens.com/didier-stevens-suite/
- Proxy setup on VMware client to monitor traffic : https://docs.vmware.com/en/VMware-Workstation-Player-for-Windows/16.0/com.vmware.player.win.using.doc/GUID-FAF3EB34-41A4-404D-B841-593D55765A77.html
- Any other tools you might find useful during the analysis such as this package by @mentebinaria : https://github.com/mentebinaria/retoolkit?s=09
- https://sourceforge.net/projects/fakenet/
- https://www.mandiant.com/resources/greater-visibilityt
- https://malwarearchaeology.com/cheat-sheets
- https://www.youtube.com/watch?v=IKTpKCIbv3M&list=PL_mJOmq4zsHYod2PeZLLljkeXwKttSF_o&index=7
- configuration de sysmon

Et évidemment installer l'agent elastic

## Installer elasticsearch avec un serveur debian
Documentation concernant la suite elasticsearch et tout les programmes tournant autour (suit ELK, elastic security...)
> what is kibana ? : https://fr.wikipedia.org/wiki/Kibana </br>
> what is elasticsearch ? : https://fr.wikipedia.org/wiki/Elasticsearch

### Installation de la suite ELK open source et ajout de Elastic security dans kibana
> DW source : https://www.elastic.co/fr/start </br>
> DW source : https://www.elastic.co/fr/campaigns/security-only-from-elastic?elektra=organic&storm=CLP&rogue=free-and-open-gic </br>
> Requierments : https://help.relativity.com/10.2/Content/Installing_and_Upgrading/System_requirements/Elasticsearch_system_requirements.htm </br>
> Installations instructions : https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html#install-elasticsearch </br>

#### Caractéristique de la VM pour les tests :
- OS : Debian 11 GUI GNOME + utilitaires basiques du système.
- Ram /!\ 2go insuffisant, préférer plus de 8go. j'ai mis 16.
- Processeur, préférez 4 coeurs logiques. j'ai mis 16.

#### Procédure d'installation sur debian
> source : https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html</br>
> source : https://www.elastic.co/guide/en/kibana/current/deb.html
1) téléchargez les sources elastik et kibana, et installez le tout :
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt-get update && sudo apt-get install elasticsearch
sudo apt-get update && sudo apt-get install kibana
```
2) une fois installé, enregistrez le programme elastik dans le système pour qu'il démarre automatiquement, et activer le serveur :
```
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
sudo systemctl start elasticsearch.service
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable kibana.service
sudo systemctl start kibana.service
```
3) vérifiez le fonctionnement de l'api elastik en requêtant "localhost:9200" (via navigateur, ou requête curl GET)
4) vérifiez le fonctionnement de kibana en requêtant localhost:5601 via le navigateur de la VM.
5) Pour un serveur de développement, si tout est exécuté en local sur la VM, la configuration de base est actuellement bonne. On peut passer à l'utilisation d'elastiksearch.

#### Première connexion web au service kibana

> source : https://www.elastic.co/guide/en/kibana/current/access.html </br>
> Source : https://www.elastic.co/guide/en/elasticsearch/reference/7.16/modules-network.html

La première connection au service elasticsearch + kibana se fait sur un navigateur via l'url `localhost:5601`.
- Il est possible d'ajouter des données directement depuis la première page. Nous n'allons pas faire cela. 
- Vérifier les pages suivantes : `localhost:5601/status` pour voir si tout est ok.

Vérifier que la VM est bien configuré au niveau du réseau en `host only` </br>
pour la configuration réseau, on modifieras dans l'emplacement aproporié les options réseau d'elastik : </br>
`nano /etc/elasticsearch/elasticsearch.yml`
```
network.bind_host: ["192.168.220.185", "localhost"]
network.publish_host: 192.168.220.185
```

- Note pour la suite : penser à sécuriser l'accès avec un mot de passe : l'app viens préinstallé sans portail d'authentification.
- Penser à ouvir l'accès à un réseau local pour faire remonter les données d'un agent elastic à partir d'une secondde VM.
- La prochaine fois c'est la configuration de elastik et de kibana pour acccéder au service depuis l'extérieur de la VM.

